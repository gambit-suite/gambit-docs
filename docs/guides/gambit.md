# GAMBIT


---


---

## Technical Details

### K-mer-based representation of the genomes

A GAMBIT signature is a compressed representation of a genome sequence that supports the efficient calculation of the **GAMBIT genomic distance metric**. It is defined as the set of *k*-mers present in the genome which occur immediately following a fixed prefix sequence. **GAMBIT finds all 11-mers in a genome assembly that immediately follows the prefix sequence ATGAC**.

This allows not only thousands of genomes to be represented in a relatively small (~3GB) database, but the comparison of the query genome to the set of references provided in the used GAMBIT database to be performed very fast.

!!! warning "Taxonomy information"
    The **GAMBIT database** used for classification consists of pre-calculated signatures for the reference genomes along with additional genome metadata and a taxonomy tree. As of GAMBIT Prokaryotic database v2.0.0, taxonomy information is derived from the  [Genome Taxonomy Database (GTDB)](https://gtdb.ecogenomic.org/) but restricted to the genus and species ranks and subject to additional curation. The other databases have the taxonomy information derived from the [NCBI taxonomy database](https://www.ncbi.nlm.nih.gov/taxonomy).

### Distance Metric Calculation

/// html | div[style='float: left; width: 50%; padding: 20px;']
The **Jaccard Index**, also known as the Jaccard Similarity Coefficient, is a statistic used for gauging the similarity and diversity between two sample sets. It ranges from 0 to 1, where if 0 the sets have no elements in common, whereas if 1 the sets are identical. In GAMBIT, the Jaccard Index is used to compare genetic sequences.

!!! warning "Jacard Distance vs Index"
    The **Jaccard Distance**, equal to one minus the Jaccard index, shares the same properties as the Jaccard index albeit inversely. It ranges from 0 to 1, where  0 the sets are identical and if 1, the sets have no elements in common.

In GAMBIT, the Jaccard Distance is calculated between two pre-computed k-mer sets in sparse coordinate format, one representing the query genome and another the GAMBIT database.

### Built-in Species Distance Threshold

GAMBIT classifies unknown genomes by finding the distance to the closest reference genome and comparing that distance against the thresholds of the reference genome’s species and genus.

For GAMBIT Prokaryotic database v2.0.0 and above, the threshold for a given species corresponds to the maximum intra-species distance ("max intra," or diameter) ([Figure 1](#figure1)). Some species are not well separated from their closest sister taxon and, in some cases, even overlap. Such as the case of *Escherichia coli* and *Shigella sonnei* in GAMBIT’s Prokaryotic Database. In these scenarios, the species were divided into subspecies groups based on clustering of their intra-species distances, and then reporting matches to these subgroups and their parent species.

If the query genome distance is greater than the species diameter, GAMBIT attempts to report the genus. Genus diameters are computed and manually curated based on the diversity of the genus.
///

/// html | div[style='float: right; width: 50%; padding: 20px;']
!!! caption "Distribution of GAMBIT distances"
    ##### Figure 1
    ![**Figure 1: Distribution of GAMBIT distances within a species and to the nearest sister taxon in the GAMBIT reference database.** Three histograms are shown in each panel (each normalized independently). The green histogram represents the distribution of GAMBIT distances from each reference genome in the species to the closest genome also within the same species. The blue histogram represents the distribution of GAMBIT distances for all pairwise comparisons within the species. The red histogram represents the distribution of GAMBIT distances from each genome in the species of interest to the closest genome in the species’ closest sister taxon. The dashed blue line represents the classification threshold for that species in the GAMBIT database, which in both cases was derived from the maximum intra-species distance. Panel A shows *Klebsiella pneumoniae* and its closest sister taxon *Klebsiella variicola*, panel B shows *Neisseria gonorrhoeae* and its closest sister taxon *Neisseria meningitidis*.  ****https://doi.org/10.1371/journal.pone.0277575.g004](../assets/figures/GAMBIT-distribution-of-distances.png)

    **Figure 1: Distribution of GAMBIT distances within a species and to the nearest sister taxon in the GAMBIT reference database.** Three histograms are shown in each panel (each normalized independently). The green histogram represents the distribution of GAMBIT distances from each reference genome in the species to the closest genome also within the same species. The blue histogram represents the distribution of GAMBIT distances for all pairwise comparisons within the species. The red histogram represents the distribution of GAMBIT distances from each genome in the species of interest to the closest genome in the species’ closest sister taxon. The dashed blue line represents the classification threshold for that species in the GAMBIT database, which in both cases was derived from the maximum intra-species distance. Panel A shows _Klebsiella pneumoniae_ and its closest sister taxon _Klebsiella variicola_, panel B shows _Neisseria gonorrhoeae_ and its closest sister taxon _Neisseria meningitidis_. 
    
    Sourced from <https://doi.org/10.1371/journal.pone.0277575.g004>.
///

/// html | div[style='clear: both;']
///

/// html | div[style='float: left; width: 50%; padding: 20px;']

### GAMBIT distances correlate with **sequence identity**

Average Nucleotide Identity (ANI) has been the benchmark for nucleic acid comparisons and was used as a baseline measure of genomic similarity to validate the GAMBIT distance metric. ANI is generally used to determine similarity at the species or genus level with thresholds above 0.92 being optimal for species-level calls.

The ANI values were compared against GAMBIT distances for all pairs of genomes in each of the four data sets:

!!! dna "Test sets for GAMBIT distance versus ANI"
    | Set | Number of Genomes | Phylogenetic Diversity | Assembly Quality | Reference |
    | --- | --- | --- | --- | ---|
    | Set 1 | 492 | Low (_E. coli_ only) | Medium | <https://doi.org/10.1186/s13059-016-0997-x> |
    | Set 2 | 70 | High (muliple phyla) | High | <https://doi.org/10.1073/pnas.0308653100> |
    | Set 3 | 88 | High (multiple phyla) | Medium | <https://doi.org/10.1371/journal.pone.0277575> |
    | Set 4 | 604 | High (multiple phyla) | Medium | <https://doi.org/10.1371/journal.pone.0277575> |
  
Spearman correlation was high in all four data sets ([Figure 2](#figure2)) (Set 1 = -0.977; Set 2 = -0.968; Set 3 = -0.969; Set 4 = -0.979) for comparisons in which the ANI was reported by the FastANI tool (100%, 5.59%, 7.42% and 47.4%), revealing a nearly monotonic relationship between GAMBIT distance and ANI.
///

/// html | div[style='float: right; width: 50%; padding: 20px;']
!!! caption "Relationship between GAMBIT distance and ANI"
    ##### Figure 2 
    ![**Figure 2: Relationship between GAMBIT distance and ANI (Average Nucleotide Identity).**  The relationship is nonlinear but very close to monotonic as measured by Spearman correlation (shown in the bottom left corner of each subplot). ANI was calculated using the [FastANI](https://github.com/ParBLiSS/FastANI) tool with default parameter values. GAMBIT distances were calculated for all sets using the same parameter (k = 11, prefix = ATGAC). As FastANI only reports ANI values greater than ~80%, the fraction of total pairwise comparisons shown here were 100%, 5.5%, 7.4% and 47.4% for data sets 1–4 respectively. https://doi.org/10.1371/journal.pone.0277575.g001](../assets/figures/GAMBIT-distance-vs-ani.png)

    **Figure 2: Relationship between GAMBIT distance and ANI (Average Nucleotide Identity).**  The relationship is nonlinear but very close to monotonic as measured by Spearman correlation (shown in the bottom left corner of each subplot). ANI was calculated using the [FastANI](https://github.com/ParBLiSS/FastANI) tool with default parameter values. GAMBIT distances were calculated for all sets using the same parameter (k = 11, prefix = ATGAC). As FastANI only reports ANI values greater than ~80%, the fraction of total pairwise comparisons shown here were 100%, 5.5%, 7.4% and 47.4% for data sets 1–4 respectively. 
    
    Sourced from <https://doi.org/10.1371/journal.pone.0277575.g001>.
///

/// html | div[style='clear: both;']
///

---


## Other Resources

- [Original GAMBIT publication](https://doi.org/10.1371/journal.pone.0277575)
- [GAMBIT Fungal Database publication](https://doi.org/10.3389/fpubh.2023.1198213)
- [GAMBIT Software GitHub](https://github.com/jlumpe/gambit/tree/master) - repository of GAMBIT software
- [GAMBIT suite GitHub](https://github.com/gambit-suite) - tools for working with GAMBIT including GAMBITdb for automated GAMBIT database creation

---

## References

Please cite the article below when using the **GAMBIT software and/or GAMBIT RefSeq Curated Database v1.0.0:**

> Lumpe J, Gumbleton L, Gorzalski A, Libuit K, Varghese V, et al. (2023) GAMBIT (Genomic Approximation Method for Bacterial Identification and Tracking): A methodology to rapidly leverage whole genome sequencing of bacterial isolates for clinical identification. PLOS ONE 18(2): e0277575. <https://doi.org/10.1371/journal.pone.0277575>

Please cite the reference below when using the **GAMBIT Fungal Database v0.2.0:**

> Ambrosio III, F. J., Scribner, M. R., Wright, S. M., Otieno, J. R., Doughty, E. L., Gorzalski, A., ... & Hess, D. (2023). TheiaEuk: a species-agnostic bioinformatics workflow for fungal genomic characterization. _Frontiers in Public Health_, _11_. <https://doi.org/10.3389/fpubh.2023.1198213>