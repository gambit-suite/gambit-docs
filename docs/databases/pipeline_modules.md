# Module Overview

The gambitdb-nf pipeline is composed of several specialized modules that work together to create a high-quality GAMBIT database. This page provides an overview of all modules and their roles in the pipeline.

## Pipeline Architecture

The pipeline follows a modular architecture with three main categories:

1. **Data Ingestion** - Parsing and downloading
2. **Processing** - Quality control, distance calculations, and downsampling
3. **Database Creation** - Final curation and database assembly

## Core Modules

### Data Ingestion Modules

#### GTDB_PARSER

**Purpose**: Parse GTDB metadata and filter genomes based on quality criteria

**Inputs**:
- GTDB metadata TSV file

**Outputs**:
- Species taxa file
- Filtered genome assembly metadata
- Representative genomes list

**Key Parameters**:
- `checkm_completeness`: Minimum genome completeness (default: 97)
- `checkm_contamination`: Maximum contamination (default: 3)
- `max_contigs`: Maximum number of contigs (default: 100)
- `minimum_genomes_per_species`: Minimum genomes per species (default: 2)
- `use_ncbi_taxonomy`: Whether or not to source taxonomy from NCBI
- `ncbi_whitelist`: List of only SPECIFIC species or genra to source from NCBI

#### BULK_DOWNLOADER

**Purpose**: Download genome assemblies from NCBI in parallel batches

**Inputs**:
- Genome assembly metadata

**Outputs**:
- Downloaded FASTA files
- Assembly metadata for downloaded genomes

**Key Parameters**:
- `max_workers`: Parallel download workers (default: 8)
- `batch_size`: Genomes per batch (default: 1000)
- `api_key`: NCBI API key for higher rate limits
- `max_retries`: Retry attempts per batch (default: 3)

### Processing Modules

#### GENERATE_SPECIES_LISTS

**Purpose**: Organize genomes into species-specific directories

**Inputs**:
- Assembly metadata
- Species taxa file

**Outputs**:
- Species-specific file lists

#### GAMBIT_DISTS_BY_SPECIES

**Purpose**: Calculate GAMBIT k-mer signatures and distance matrices for each species

**Inputs**:
- Species file directories
- Genome FASTA files

**Outputs**:
- K-mer signatures per species
- Distance matrices per species
- Diameter calculations per species

**Note**: This module runs in parallel for all species, making it highly scalable.

#### GAMBIT_DISTS_COMBINED

**Purpose**: Calculate combined distance matrix for all filtered genomes

**Inputs**:
- Combined genome set after downsampling/filtering

**Outputs**:
- Combined signatures
- Combined distance matrix (CSV and NumPy formats)
- Combined diameters

#### GAMBIT_CURATE

**Purpose**: Quality control and outlier detection using distance-based methods

**Inputs**:
- Assembly directory
- Distance matrix
- Diameter calculations
- Genome metadata

**Outputs**:
- Curated genome metadata
- Curated species file

**Features**:
- Identifies genomic outliers
- Validates species assignments
- Ensures database quality

### Optimization Modules

#### ANALYZE_CURATED

**Purpose**: Analyze curated results to identify species requiring downsampling

**Inputs**:
- Curated species metadata

**Outputs**:
- Species analysis reports
- Downsample target lists

#### STRATIFIED_DOWNSAMPLE

**Purpose**: Stratified based downsampling method for genome counts for overrepresented species

**Inputs**:
- Distance matrices
- Curated metadata
- Representative genomes
- Downsample targets

**Outputs**:
- Keep genomes list
- Remove genomes list

**Key Parameters**:
- `downsample_threshold`: Minimum genomes to trigger downsampling (default: 1000)
- `k`: Number of clusters (default: 100)
- `n_pairs`: Target pairs to select (default: 500)

**Algorithm**:
1. Bin genomes using distance matrix
2. Select representative from each cluster
3. Ensure diversity preservation
4. Maintain genomes responsible for min/max distance thresholds and reference genomes

#### FILTER_COMBINE_GENOMES

**Purpose**: Remove downsampled genomes and combine filtered dataset

**Inputs**:
- FASTA directory
- Assembly metadata
- Species taxa
- Remove genomes list

**Outputs**:
- Filtered combined dataset

### Utility Modules

#### COMBINE_ANALYSIS_RESULTS

**Purpose**: Aggregate analysis results across all species

**Inputs**:
- Per-species analysis outputs
- Downsample targets

**Outputs**:
- Combined species analysis
- Combined downsample targets

#### ADD_GENUS_ROWS

**Purpose**: Add genus-level entries to enable genus-level classification

**Inputs**:
- Species taxon file

**Outputs**:
- Species file with genus rows

### Database Creation Modules

#### CREATE_GAMBIT_DB

**Purpose**: Assemble the final GAMBIT database

**Inputs**:
- Curated genome metadata
- Species taxon file (with genus rows)
- K-mer signatures

**Outputs**:
- GAMBIT database file (.gdb)
- GAMBIT signatures file (.gs)

**Key Parameters**:
- `db_key`: Database identifier
- `db_version`: Database version
- `db_author`: Database creator
- `db_date`: Creation date

## Module Dependencies

The modules follow this general flow:

```
GTDB_PARSER → BULK_DOWNLOADER → GENERATE_SPECIES_LISTS
                                         ↓
                                GAMBIT_DISTS_BY_SPECIES
                                         ↓
                                  GAMBIT_CURATE
                                         ↓
                                  ANALYZE_CURATED
                                         ↓
                              STRATIFIED_DOWNSAMPLE (optional)
                                         ↓
                              FILTER_COMBINE_GENOMES
                                         ↓
                              GAMBIT_DISTS_COMBINED
                                         ↓
                                  GAMBIT_CURATE
                                         ↓
                                  ADD_GENUS_ROWS
                                         ↓
                                 CREATE_GAMBIT_DB
```

## Workflow Variants

### GAMBITDB_SIMPLE

Uses a subset of modules for straightforward database creation without downsampling:

- Skips species-level processing
- Directly processes combined dataset
- Faster for smaller datasets

### GAMBITDB_DOWNSAMPLE

Uses the complete module suite with downsampling optimization:

- Species-level parallel processing
- Intelligent downsampling
- Optimal for large GTDB releases

## Module Documentation

For detailed information about specific modules:

- [Create GAMBIT Database](create_gambit_db.md)

## Resource Requirements

Different modules have different resource profiles:

| Module | CPU | Memory | Time | Scalability |
|--------|-----|--------|------|-------------|
| GTDB_PARSER | Low | Low | Fast | Linear |
| BULK_DOWNLOADER | Medium | Low | Variable | Parallel |
| GAMBIT_DISTS_BY_SPECIES | Medium | Medium | Medium | Parallel per species |
| GAMBIT_CURATE | Medium | Medium | Fast | Per species/combined |
| STRATIFIED_DOWNSAMPLE | Medium | High | Medium | Per large species |
| CREATE_GAMBIT_DB | Low | Medium | Fast | Single |

Resource allocations can be adjusted in `conf/base.config`.