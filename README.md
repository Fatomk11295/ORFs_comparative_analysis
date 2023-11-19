# Comparative analyses of Open Reading Frames (ORFs) between pathogenic and nonpathogenic Staphylococci species

## Table of contents
* Introduction
* Extraction, filtration, and categorizing of ORFs 
* Annotation
* Conservation test
* Function prediction
* Explore neighboring genes 
* Explore a candidate ORF

### Introduction

This repository guides analyses in the publication "Identification of pathogenic-specific open reading frames in staphylococci species".

### Extraction, filtration, and categorizing of ORFs
The pipeline involves several steps to ensure accurate and meaningful results. Below is an overview of the pipeline stages:

1. **Genomes Selection:**
   Species known for their pathogenicity were chosen, including S. aureus Mu3, S. lugdunensis HKU09-01, S. haemolyticus JCSC1435, S. saprophyticus ATCC 15305, and S. schleiferi strain 1360-13. Nonpathogenic species included S. carnosus TM300, S. cohnii SNUDS-2, S. warneri SG1, S. nepalensis DSM 15150, and S. pasteuri JS7.

   **Accession numbers:**
   
         •	S. aureus Mu3 (GCA_000010445.1)
   
         •	S. lugdunensis HKU09-01 (GCA_000025085.1)
   
         •	S. haemolyticus JCSC1435 (GCA_000009865.1)
   
         •	S. saprophyticus ATCC 15305 (GCA_000010125.1)
   
         •	S. schleiferi strain 1360-13 (GCA_001188855.1)
   
         •	S. carnosus TM300 (GCA_000009405.1)
   
         •	S. cohnii SNUDS-2 (GCA_001990205.1)
   
         •	S. warneri SG1 (GCA_000332735.1)
   
         •	S. nepalensis DSM 15150 (GCA_002902745.1)
   
         •	S. pasteuri JS7 (GCA_002442915.1)

3. **Data Collection:**
   Download the whole genome sequence for the selected species from [NCBI's FTP server](https://ftp.ncbi.nlm.nih.gov). You can find full specification about the WGS data for the selected species in this [file](https://docs.google.com/spreadsheets/d/1wd9hzx6mVgmB8F8CK_Etvh1MnovFnqct/edit?usp=sharing&ouid=103975173682819978105&rtpof=true&sd=true).

4. **ORF Extraction:**
   We employed the [EMBOSS getorf algorithm](https://www.bioinformatics.nl/cgi-bin/emboss/getorf) to extract ORFs from the selected genomes. We selected the optional qualifier **-find [1]** to identify the translation of ORFs in the regions between the start and stop codons.

5. **ORF Filtering:**
   Extracted ORFs were filtered based on size, discarding any ORF shorter than ten amino acids (aa). Moreover, 

6. **Categorization:**
   We categorized the ORFs  into five groups based on their presence in the tested genomes: 
   * found in all tested genomes.
   * found in all pathogenic tested genomes.
   * found in all nonpathogenic tested genomes.
   * found in some pathogenic tested genomes.
   * found in some nonpathogenic tested genomes.

The following image presents the filtration and categorizing process.

![figure_19_upscaled](https://github.com/Fatomk11295/ORFs_comparative_analysis/blob/main/images/figure_19_upscaled%20(1).png).
