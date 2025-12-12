# GAMBIT Database Creation

GAMBIT (Genomic Approximation Method for Bacterial Identification and Tracking) incorporates k-mer based strategy for the identification of taxonomic information with a highly curated searchable database.

A GAMBIT databases consist of two files:

1. A **signatures file** containing the GAMBIT signatures (compressed representations) of all genomes represented in the database; 
2. A **metadata file** relating the represented genomes to their genome accessions, taxonomic identifications, and species thresholds.

The goal in creating a database for GAMBIT is two-fold:

- Genomes representing each species in the database must contain enough distinction from other species so that similarity thresholds can be extracted;
- The highest level of confidence is obtained that a genome in the database is actually from the species that matched its labelled identification.

<div class="grid cards" markdown>

-   :material-magnify-expand: **GAMBIT allows for rapid taxonomic identification of microbial pathogens.**

    ---

    The GAMBIT database is designed to facilitate the exploration and analysis of genomic data from a wide variety of prokaryotic or fungal isolates. It integrates and annotates genomic information based on information from curated sources. Several sources of complete and draft genomic sequences exist, with the most common being [RefSeq](https://www.ncbi.nlm.nih.gov/refseq/), [GenBank](https://www.ncbi.nlm.nih.gov/genbank/) and [GTDB](https://gtdb.ecogenomic.org/). Alternative sources, such as [BakRep](https://bakrep.computational.bio/), can also be used as long as taxonomic information is available.

-   :material-database-check: **Several pre-computed GAMBIT databases are available for prokaryotic and fungal genomes.**

    ---

    The full list of databases available can be consulted [here](../databases/overview.md), with information on what curation steps were followed and what genomes are included.

</div>

## Database Creation Process

### Creating a GAMBIT database from a pre-curated list of genomes - GTDB and GAMBITdb-nf

The creation and curation of a GAMBIT database is a laborious process which involves sourcing genomic information, setting minimum quality thresholds, and finally building a signature and a database file.

!!! dna "Sourcing Genome Information from GTDB"
    As of [v2.0.0 of the GAMBIT Prokaryotic database](../databases/gambit_prokaryotic.md#gambit-gtdb-database-v200), [GTDB](https://gtdb.ecogenomic.org/) is the selected source of quality information for genomes sourced from [RefSeq](https://www.ncbi.nlm.nih.gov/refseq/) and [GenBank](https://www.ncbi.nlm.nih.gov/genbank/). Automation is available through the [GAMBITdb-nf](https://github.com/gambit-suite/gambitdb-nf) which takes as input a GTDB release metadata spreadsheet including information on taxonomy and assembly quality metrics. GTDB’s release spreadsheets are available at [https://data.gtdb.ecogenomic.org/releases](https://data.gtdb.ecogenomic.org/releases/). Taxonomic information can be sourced from [NCBI Taxonomy](https://www.ncbi.nlm.nih.gov/taxonomy) ofr [GTDB](https://gtdb.ecogenomic.org/).

---

#### GAMBITdb-nf 

[GAMBITdb-nf](https://github.com/gambit-suite/gambitdb-nf) is a [Nextflow](https://www.nextflow.io/) pipeline for creating and maintaining GAMBIT databases from [GTDB (Genome Tree Database)](https://gtdb.ecogenomic.org/) metadata. This pipeline automates the entire process of database creation, from quality filtering and genome downloading to k-mer signature generation and strategic downsampling.

!!! tip "Key Features"
    - **Automated Quality Control**: Filter genomes based on [CheckM2](https://github.com/chklovski/CheckM2) completeness, contamination, and assembly quality
    - **Efficient Bulk Downloading**: Parallel download of genome assemblies from [NCBI](https://www.ncbi.nlm.nih.gov/) with checkpoint support
    - **Smart Downsampling**: Stratified downsampling for large species clusters to optimize database size
    - **Flexible Workflows**: Choose between simple and downsampling workflows based on your needs
    - **Comprehensive Monitoring**: Built-in execution reports and detailed logging
    - **Container Support**: Works with [Docker](https://www.docker.com/), [Singularity](https://docs.sylabs.io/guides/3.5/user-guide/introduction.html), [Conda](https://anaconda.org/anaconda/conda), [Podman](https://podman.io/), or [Apptainer](https://apptainer.org/)

!!! dna "Support"
    - [GitHub Repository](https://github.com/gambit-suite/gambitdb-nf)
    - [Report Issues](https://github.com/gambit-suite/gambitdb-nf/issues)

[GAMBITdb-nf](https://github.com/gambit-suite/gambitdb-nf) provides two main workflows:

<div class="grid cards" markdown>

-   **GAMBITDB_SIMPLE**

    ---

    A streamlined workflow for **creating GAMBIT databases without downsampling**. 
    <br>
    This version is best for smaller datasets or for when you want to include all available genomes.

-   **GAMBITDB_DOWNSAMPLE**

    ---

    An advanced workflow with **intelligent downsampling for large species clusters**. 
    <br>
    This version is ideal for comprehensive GTDB releases where some species have thousands of genomes.

</div>

The pipeline produces:

- **GAMBIT Database**: Ready-to-use database files for GAMBIT analysis
- **K-mer Signatures**: Genomic signatures for all included genomes
- **Distance Matrices**: Pairwise genomic distances
- **Quality Reports**: Curation metadata and analysis results
- **Execution Reports**: Resource usage and pipeline performance metrics

---
