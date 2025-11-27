### GAMBIT Prokaryotic Databases

As of [v2.0.0](#gambit-gtdb-database-v200), the GAMBIT Prokaryotic Database is built iteratively over a [Genome Taxonomy Database (GTDB)](https://gtdb.ecogenomic.org/) release, starting with the species with the most publicly available genomes.

!!! tip "Database Access"
    Please note that all GAMBIT databases are located in a ["Requester Pays" GCP bucket](https://cloud.google.com/storage/docs/requester-pays).

    A billing project **must** be provided in the request to download; otherwise, the following links and GS URIs will not work.

#### GAMBIT GTDB Database v2.1.0

??? toggle "Database Details"

    This database is a **minor update** to the v2.0.1 database. This database is identical to the v2.0.1 database, **except for the following modifications**.
    
    1. Genomes representing *Salmonella enterica* subspecies houtenae and diarizonae were added to the database.
        a. Rationale: In the v2.0.0 and v2.0.1 databases, no genomes representing these subspecies are present, therefore query genomes representing these subspecies were not reliably classifed as *Salmonella enterica*.
    2. The *Salmonella arizonae* species was modified to be a subspecies of *Salmonella enterica*.
        a. Rationale: While GTDB classifies *Salmonella arizonae* as its own species due to its divergence from other Salmonella species, NCBI considers *Salmonella arizonae* a subspecies of *Salmonella enterica*. *Salmonella enterica* is also the typical naming convention within public health laboratories, therefore we have renamed the species to align with user preference.
    3. The following genomes below were removed. 
        a. Rationale: These genomes are currently named as *Shigella* species in NCBI, but are actually *Escherichia coli* according to the best match type strain using ANI. Their removal from the database prevents false assignment of *Echerichia coli* query genomes to *Shigella* species.

        GCF_002247485.1 
        GCF_002248245.1
        GCF_002249025.1
        GCF_002246815.1
        GCF_001064675.1
        GCF_022494155.1
        GCF_022494015.1
        GCF_022494095.1
        GCF_022494415.1   

    **Database Files**

    These database files are hosted in a public "Requester Pays" Google bucket by Theiagen Genomics:

    **GS URI (for [Terra.bio](https://terra.bio) usage):**

    - `gs://gambit-databases-rp/2.1.0/gambit-metadata-2.1.0-20250808.gdb`
    - `gs://gambit-databases-rp/2.1.0/gambit-signatures-2.1.0-20250808.gs`

    **HTTPS URL (for local download):**

    - <https://storage.cloud.google.com/gambit-databases-rp/2.1.0/gambit-metadata-2.1.0-20250808.gdb>
    - <https://storage.cloud.google.com/gambit-databases-rp/2.1.0/gambit-signatures-2.1.0-20250808.gs>

#### GAMBIT GTDB Database v2.0.1

??? toggle "Database Details"

    This database is a **patch update** to the v2.0.0 database. This database is identical to the v2.0.0 database **except that the following genomes were removed**. 

        GCF_003977345.1
        GCF_003977375.1
        GCF_004025385.1
        GCF_002249045.1
        GCF_004402105.1
        GCF_003977405.1
        GCF_003985005.1
        GCF_002246205.1
        GCF_003977245.1
        GCF_007197595.1
        GCF_003977285.1
        GCF_001063095.1
        GCF_002248705.1

    These genomes currently named as *Shigella* species in NCBI, but are actually *Escherichia coli* according to the best match type strain using ANI. Their removal from the database prevents false assignment of *Echerichia coli* query genomes to *Shigella* species.

    **Database Files**

    These database files are hosted in a public "Requester Pays" Google bucket by Theiagen Genomics:

    **GS URI (for [Terra.bio](https://terra.bio) usage):**

    - `gs://gambit-databases-rp/2.0.0/gambit-metadata-2.0.1-20250505.gdb`
    - `gs://gambit-databases-rp/2.0.0/gambit-signatures-2.0.1-20250505.gs`

    **HTTPS URL (for local download):**

    - <https://storage.cloud.google.com/gambit-databases-rp/2.0.0/gambit-metadata-2.0.1-20250505.gdb>
    - <https://storage.cloud.google.com/gambit-databases-rp/2.0.0/gambit-signatures-2.0.1-20250505.gs>

#### GAMBIT GTDB Database v2.0.0

??? toggle "Database Details"
    This database is a **major update** to the Curated v1.3.0 database. This iteration of the GAMBIT database relies upon the [Genome Taxonomy Database](https://gtdb.ecogenomic.org/) (GTDB), an initiative to establish a standardised microbial taxonomy based on genome phylogeny. The genomes used to construct the phylogeny are obtained from [RefSeq](https://www.ncbi.nlm.nih.gov/refseq/) and [GenBank](https://www.ncbi.nlm.nih.gov/genbank/), independently quality-controlled using [CheckM](https://github.com/Ecogenomics/CheckM/wiki) before inclusion in GTDB.

    This database was computed from [GTDB Release 214.1](https://gtdb.ecogenomic.org/stats/r214) as of April 28th, 2023. 

    - **Automated curation efforts**
        
        The following curation steps were followed for all species:
        
        - The candidates for an existing genus were collapsed (e.g genus_A, genus_B becomes genus)
        
        The following species were updated:
        
        - *Shigella* sp*.*
            - This genus is not present in GTDB  as it is collapsed under *Escherichia coli;*
            - All Shigella genomes in RefSeq were added to the database with no clustering using default quality criteria.
        - *Mycolicibacterium/Mycolicibacter/Mycolicibacillus/Mycobacteroides/Mycobacterium* sp.
            - All genomes available were used.
        - *Tropheryma whipplei*
            - This species has a low completeness score of 75%;
            - The CheckM completeness score was lowered to 70% for genomes belonging to this species.

    **Database Files**

    These database files are hosted in a public "Requester Pays" Google bucket by Theiagen Genomics:

    **GS URI (for [Terra.bio](https://terra.bio) usage):**

    - `gs://gambit-databases-rp/2.0.0/gambit-metadata-2.0.0-20240628.gdb`
    - `gs://gambit-databases-rp/2.0.0/gambit-signatures-2.0.0-20240628.gs`

    **HTTPS URL (for local download):**

    - <https://storage.cloud.google.com/gambit-databases-rp/2.0.0/gambit-metadata-2.0.0-20240628.gdb>
    - <https://storage.cloud.google.com/gambit-databases-rp/2.0.0/gambit-signatures-2.0.0-20240628.gs>

    **Taxa included in the GAMBIT database**

    Summary of species represented in the database with number of genomes representing each species and the species threshold:

    - <https://storage.cloud.google.com/gambit-databases-rp/2.0.0/gambit-taxa-2.0.0-20240628.tsv>
    
        Note: Species with a threshold of "0" have been sub-speciated. Subspecies are not listed in this table.

#### GAMBIT RefSeq Curated Database v1.3.0

??? toggle "Database Details"
    This database is a **patch update** to the Curated v1.2.0 database. In addition to all of the species included in the v1.2.0 database below, this database replaces all species in the **_Mycobacterium_, _Mycolicibacterium_, _Mycobacteroides_, and _Mycolicibacter_** genera with the available genomes in RefSeq as of October 16th, 2023.

    - **Manual curation efforts**
        
        The following species were updated:
        
        - *Mycolicibacterium/Mycolicibacter/Mycolicibacillus/Mycobacteroides/Mycobacterium* sp.
            - All genomes available were used

    **Database Files**

    These database files are hosted in a public "Requester Pays" Google bucket by Theiagen Genomics:

    **GS URI (for [Terra.bio](https://terra.bio) usage):**

    - `gs://gambit-databases-rp/1.3.0/gambit-metadata-1.3-231016.gdb`
    - `gs://gambit-databases-rp/1.3.0/gambit-signatures-1.3-231016.gs`

    **HTTPS URL (for local download):**

    - <https://storage.cloud.google.com/gambit-databases-rp/1.3.0/gambit-metadata-1.3-231016.gdb>
    - <https://storage.cloud.google.com/gambit-databases-rp/1.3.0/gambit-signatures-1.3-231016.gs>

    **Taxa included in the GAMBIT database**

    Summary of species represented in the database with number of genomes representing each species and the species threshold:

    - <https://storage.cloud.google.com/gambit-databases-rp/1.3.0/gambit-1.3-231016-taxa-list.txt>
        
        Note: Species with a threshold of "0" have been sub-speciated. Subspecies are not listed in this table.

#### GAMBIT RefSeq Curated Database v1.2.0

??? toggle "Database Details"
    This database is a **patch update** to the RefSeq Curated v1.1.0 database. In addition to all of the species included in the v1.1.0 database below, this database includes new species that were under-represented as of August 11th, 2023.

    - **Automated curation efforts**
       
        Automated addition of new species to the database that are genetically distant from all current species in the v1.1.0 GAMBIT database. 
        
        Genomes represented in the Genome Taxonomy Database ([GTDB](https://gtdb.ecogenomic.org/)) were added. These genomes predominantly originate from the RefSeq and GenBank databases with taxonomic metadata curated by GTDB. Any genomes added to the GAMBIT database from GTDB are added with the metadata from GTDB.
            
        - Genomes added from GTDB include the following species:
          
            [gambit-list-of-new-species-db-v1_2_0.txt](../assets/files/gambit-list-of-new-species-db-v1_2_0.txt)
                
    - **Manual curation efforts**
       
        Manually curated updates to several taxa relevant to public health. All genomes representing the taxa below were removed and replaced with the RefSeq genomes representing each species as of August 11th, 2023.
        
        - *Citrobacter, Providencia, Hafnia, Neisseria, Proteus, Achromobacter, Aeromonas, Bacillus, Brucella, Afipia, Burkholderia, Paraburkholderia, Corynebacterium, Morganella*

    **Database Files**

    These database files are hosted in a public "Requester Pays" Google bucket by Theiagen Genomics:

    **GS URI (for [Terra.bio](https://terra.bio) usage):**

    - `gs://gambit-databases-rp/1.2.0/gambit-metadata-1.2-231002.gdb`
    - `gs://gambit-databases-rp/1.2.0/gambit-signatures-1.2-231002.gs`

    **HTTPS URL (for local download):**

    - <https://storage.cloud.google.com/gambit-databases-rp/1.2.0/gambit-metadata-1.2-231002.gdb>
    - <https://storage.cloud.google.com/gambit-databases-rp/1.2.0/gambit-signatures-1.2-231002.gs>

    **Taxa included in the GAMBIT database**

    Summary of species represented in the database with number of genomes representing each species and the species threshold:

    - <https://storage.cloud.google.com/gambit-databases-rp/1.2.0/gambit-1.2-231002-taxa-list.txt>
        Note: Species with a threshold of "0" have been sub-speciated. Subspecies are not listed in this table.

#### GAMBIT RefSeq Curated Database v1.1.0

??? toggle "Database Details"
    This database is a **patch update** to the RefSeq Curated v1.0.0 database. In addition to all of the species included in the v1.0.0 database below, this database replaces all species in the **Enterobacter, Legionella, and Vibrio genera** with the available genomes in RefSeq as of April 17th, 2023.

    **Database Files**

    These database files are hosted in a public "Requester Pays" Google bucket by Theiagen:

    **GS URI (for [Terra.bio](https://terra.bio) usage):**

    - `gs://gambit-databases-rp/1.1.0/gambit-metadata-1.1-230417.gdb`
    - `gs://gambit-databases-rp/1.1.0/gambit-signatures-1.1-230417.gs`

    **HTTPS URL (for local download):**

    - <https://storage.cloud.google.com/gambit-databases-rp/1.1.0/gambit-metadata-1.1-230417.gdb>
    - <https://storage.cloud.google.com/gambit-databases-rp/1.1.0/gambit-signatures-1.1-230417.gs>

    **Taxa included in the GAMBIT database**

    Summary of species represented in the database with number of genomes representing each species and the species threshold:

    - <https://storage.cloud.google.com/gambit-databases-rp/1.1.0/gambit-1.1-230417-taxa-list.txt>
        
        Note: Species with a threshold of "0" have been sub-speciated. Subspecies are not listed in this table.

#### GAMBIT RefSeq Curated Database v1.0.0

??? toggle "Database Details"
    The GAMBIT RefSeq Curated v1.0.0 database was used for the analysis described in the [GAMBIT publication](https://doi.org/10.1371/journal.pone.0277575). This database was constructed based on the available genomes in RefSeq as of July 1st, 2016.  Genomes that did not have associated genus and/or species were removed. Additionally, at least two separate sequenced isolates for a given species were required in order to determine the classification threshold.  

    - **Manual curation efforts**
        
        Ambiguous genomes were removed if they met any of the following criteria: 
        
        1. A genome that did not cluster well with the majority of the other genomes within their species;
        2. A genome that clustered well with some members of their species but also several members of another species in the database<
        3. A genome that did not cluster well with any genomes in the database.

    **Database Files**

    These database files are hosted in a public "Requester Pays" Google bucket by Theiagen:

    **GS URI (for [Terra.bio](https://terra.bio) usage):**

    - `gs://gambit-databases-rp/1.0b2/gambit-genomes-1.0b2-rev2-211116.db`
    - `gs://gambit-databases-rp/1.0b2/gambit-signatures-1.0b1-210719.h5`

    **HTTPS URL (for local download):**

    - <https://storage.cloud.google.com/gambit-databases-rp/1.0b2/gambit-genomes-1.0b2-rev2-211116.db>
    - <https://storage.cloud.google.com/gambit-databases-rp/1.0b2/gambit-signatures-1.0b1-210719.h5>

    **Taxa included in the GAMBIT database**

    Summary of species represented in the database with number of genomes representing each species and the species threshold:

    - <https://storage.cloud.google.com/gambit-databases-rp/1.0b2/gambit-1.0b2-rev2-211116-taxa-list.txt>
        
        Note: Species with a threshold of "0" have been sub-speciated. Subspecies are not listed in this table.
