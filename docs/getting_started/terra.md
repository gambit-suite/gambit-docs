# GAMBIT on Terra.bio

[Theiagen](https://www.theiagen.com/)’s [Public Health Bioinformatics (PHB)](https://github.com/theiagen/public_health_bioinformatics) is a suite of workflows for characterization, epidemiology and sharing of pathogen genomes. Workflows are available for viruses, bacteria, and fungi.

## Importing and using GAMBIT via the PHB workflows

The [**GAMBIT_Query_PHB**](https://dockstore.org/workflows/github.com/theiagen/public_health_bioinformatics/Gambit_Query_PHB) workflow performs taxon assignment of a genome assembly using the GAMBIT. It can be imported directly to [Terra.bio](https://terra.bio) via [Dockstore](https://dockstore.org).

Two inputs are required for the **GAMBIT_Query_PHB** workflow: a genome assembly and a sample name associated with the genome assembly. The default GAMBIT database used for taxonomic identification is the Prokaryotic [GAMBIT Database GTDB v2.1.0](#gambit-gtdb-database-v210), but alternate GAMBIT databases can be provided.

!!! tip inline end "Import workflows to [Terra.bio](https://terra.bio/):"
    **GAMBIT_Query_PHB**

    - [Gambit_Query_PHB](https://dockstore.org/workflows/github.com/theiagen/public_health_bioinformatics/Gambit_Query_PHB)
    
    **TheiaProk Workflow Series**
    
      - [TheiaProk_Illumina_PE_PHB](https://dockstore.org/workflows/github.com/theiagen/public_health_bioinformatics/TheiaProk_Illumina_PE_PHB)
      - [TheiaProk_Illumina_SE_PHB](https://dockstore.org/workflows/github.com/theiagen/public_health_bioinformatics/TheiaProk_Illumina_SE_PHB)
      - [TheiaProk_ONT_PHB](https://dockstore.org/workflows/github.com/theiagen/public_health_bioinformatics/TheiaProk_ONT_PHB)
      - [TheiaProk_FASTA_PHB](https://dockstore.org/workflows/github.com/theiagen/public_health_bioinformatics/TheiaProk_FASTA_PHB)
    
    **TheiaEuk Workflow Series**
   
      - [TheiaEuk_Illumina_PE_PHB](https://dockstore.org/workflows/github.com/theiagen/public_health_bioinformatics/TheiaEuk_Illumina_PE_PHB)

Additionally, GAMBIT is also part of the **TheiaProk** and **TheiaEuk** collection of workflows, the first dedicated to the analysis of prokaryotic data, and the second data to mycotics. The TheiaProk or TheiaEuk most appropriate for your type of input data can be imported from the Dockstore links on the right.

In both, GAMBIT is responsible for performing the taxonomic identification of the assembled sequences, which can trigger taxa-specific submodules for further genomic characterization. For TheiaProk, the default database is the Prokaryotic [GAMBIT Database GTDB v2.1.0](#gambit-gtdb-database-v210) and for TheiaEuk, the default database is the [Fungal GAMBIT Database v1.0.0](#gambit-fungal-database-v100).