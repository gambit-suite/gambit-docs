### GAMBIT Fungal Databases

!!! tip "Database Access"
    Please note that all GAMBIT databases are located in a ["Requester Pays" GCP bucket](https://cloud.google.com/storage/docs/requester-pays).

    A billing project **must** be provided in the request to download; otherwise, the following links and GS URIs will not work.

#### GAMBIT Fungal Database v1.0.0

??? toggle "Database Details"
    The GAMBIT Fungal Database v1.0.0 database was constructed based on the available genomes in RefSeq/GenBank as of December 13th, 2024. For inclusion in the database, species were required to have at least two genomes in GenBank and at least one genome representing the species in RefSeq.

    1. Species with a diameter of zero were excluded;
    2. Species with three or fewer genomes and a diameter greater than 0.75 were excluded.
    
    **Manual curation efforts**
    
     - Species were curated based on GAMBIT diameter:
     - The database was manually curated to remove highly distant genomes which were likely mislabeled.
     - Six species were divided into subspecies to ensure non-overlapping species diameters.
     - Two pairs of species were too closely related to distinguish (*Aspergillus flavus/Aspergillus oryzae* and *Aspergillus niger/Aspergillus welwitschiae*), therefore were combined.

    **Database Files**

    These database files are hosted in a public "Requester Pays" Google bucket by Theiagen:

    **GS URI (for [Terra.bio](https://terra.bio) usage):**

    - `gs://gambit-databases-rp/fungal-version/1.0.0/gambit-fungal-metadata-1.0.0-20241213.gdb`
    - `gs://gambit-databases-rp/fungal-version/1.0.0/gambit-fungal-signatures-1.0.0-20241213.gs`

    **HTTPS URL (for local download):**

    - <https://storage.cloud.google.com/gambit-databases-rp/fungal-version/1.0.0/gambit-fungal-metadata-1.0.0-20241213.gdb>
    - <https://storage.cloud.google.com/gambit-databases-rp/fungal-version/1.0.0/gambit-fungal-signatures-1.0.0-20241213.gs>

    **Taxa included in the GAMBIT database**

    360 fungal species from 176 genera are represented in the fungal database from a total of 8073 fungal genomes. A table indicating the number of genomes and species diameter for each species represented in the database is indicated below.

    [gambit-1.0.0-20241213-taxa-list.txt](../assets/files/gambit-1.0.0-20241213-taxa-list.txt)


#### GAMBIT Fungal Database v0.2.0

??? toggle "Database Details"
    The GAMBIT Fungal Database v0.2.0 database was used for the analysis described in the [TheiaEuk publication](https://doi.org/10.3389/fpubh.2023.1198213). This database was constructed based on the available genomes in GenBank as of November 30th, 2022. For inclusion in the database, species were required to have at least two genomes in GenBank and at least one genome representing the species in RefSeq.

    1. Species with a diameter of zero were excluded;
    2. Species with three or fewer genomes and a diameter greater than 0.75 were excluded.

    **Manual curation efforts**

    - Species were curated based on GAMBIT diameter:
    - The database was manually curated to remove highly distant genomes which were likely mislabeled.
    - Nine species were divided into subspecies to ensure non-overlapping species diameters.
    - Two pairs of species were too closely related to distinguish (*Aspergillus flavus/Aspergillus oryzae* and *Aspergillus niger/Aspergillus welwitschiae*), therefore were combined.

    **Database Files**

    These database files are hosted in a public "Requester Pays" Google bucket by Theiagen:

    **GS URI (for [Terra.bio](https://terra.bio) usage):**

    - `gs://gambit-databases-rp/fungal-version/0.2/221130-theiagen-fungal-v0.2.db`
    - `gs://gambit-databases-rp/fungal-version/0.2/221130-theiagen-fungal-v0.2.h5`

    **HTTPS URL (for local download):**

    - <https://storage.cloud.google.com/gambit-databases-rp/fungal-version/0.2/221130-theiagen-fungal-v0.2.db>
    - <https://storage.cloud.google.com/gambit-databases-rp/fungal-version/0.2/221130-theiagen-fungal-v0.2.h5>

    **Taxa included in the GAMBIT database**

    245 fungal species from 138 genera are represented in the fungal database from a total of 5,667 fungal genomes. A table indicating the number of genomes and species diameter for each species represented in the database is indicated below.

    [gambit-0.2.0-221130-taxa-list.tsv](../assets/files/gambit-0.2.0-221130-taxa-list.txt)