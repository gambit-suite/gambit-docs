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

    The full list of databases available can be consulted [here](./gambit.md#gambit-databases), with information on what curation steps were followed and what genomes are included.

</div>
