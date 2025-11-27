# GAMBIT Databases Overview

## GAMBIT Database Creation and Curation

The creation of a GAMBIT Database usually follows these steps:

- From a public repository, the genomes of interest are downloaded. Each taxa should have at least 2 genomes for GAMBIT diameters to be calculated;
- The downloaded genomes undergo a round of quality-control to minimize the possibility that the genomes are too fragmented, contaminated or too incomplete. Third-party tools, such as [QUAST](https://github.com/ablab/quast) and [CheckM](https://github.com/Ecogenomics/CheckM)/[BUSCO](https://busco.ezlab.org/) are used in this step;
- GAMBIT distances are calculated for all pairs of genomes, removing overlapping sequences and misclassification to increase the accuracy of GAMBIT;
- The database undergoes a curation to remove outliers and improve classification in underrepresented taxa and reflect public health usage and biological historical consensus more closely.

!!! tip "Dependent on public data"
    Please note that GAMBIT databases undergo curation and testing prior to release, but are limited by the **availability and accuracy** of sequencing data in public repositories.

Because GAMBIT databases have built-in species thresholds, genomes are included in each database version and the thresholds associated with each species are **curated** prior to release. Curation approaches may vary by GAMBIT database release but aim to ensure that **mislabeled genomes are removed** and that species are **non-overlapping**.

---

/// html | div[class="grid cards" markdown]

-   <center>[Prokaryotic Databases](gambit_prokaryotic.md){ .md-button .md-button--secondary }</center>

-   <center>[Fungal Databases](gambit_fungal.md){ .md-button .md-button--secondary }</center>

///