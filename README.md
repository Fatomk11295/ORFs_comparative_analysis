# Comparative analyses of Open Reading Frames (ORFs) between pathogenic and nonpathogenic Staphylococci species

## Table of contents
* Introduction
* Extraction, filtration and categorizing of ORFs 
* Annotation
* Conservation test
* Function prediction
* Explore neighboring genes 
* Explore a candidate ORF

### Introduction
This repository is a guide for analyses performed in the publication about finding proteins responsible for the pathogenicity of Staphylococci species.

### Extraction, filtration and categorizing of ORFs 
The pipeline involves several steps to ensure accurate and meaningful results. Below is an overview of the pipeline stages:

1. **Genomes Selection:**
   Species known for their pathogenicity were chosen, including S. aureus Mu3, S. lugdunensis HKU09-01, S. haemolyticus JCSC1435, S. saprophyticus ATCC 15305, and S. schleiferi strain 1360-13. Nonpathogenic species included S. carnosus TM300, S. cohnii SNUDS-2, S. warneri SG1, S. nepalensis DSM 15150, and S. pasteuri JS7. 

2. **Data Collection:**
   Download the whole genome sequence for the selected species from [NCBI's FTP server](https://ftp.ncbi.nlm.nih.gov). You can find full specification about the WGS data for the selected species in this [file](https://docs.google.com/spreadsheets/d/1wd9hzx6mVgmB8F8CK_Etvh1MnovFnqct/edit?usp=sharing&ouid=103975173682819978105&rtpof=true&sd=true).

3. **ORF Extraction:**
   We employed the [EMBOSS getorf algorithm](https://www.bioinformatics.nl/cgi-bin/emboss/getorf) to extract ORFs from the selected genomes. We selected the optional qualifier **-find [1]** to identify the translation of ORFs in the regions between the start and stop codons.

4. **ORF Filtering:**
   Extracted ORFs were filtered based on size, discarding any ORF shorter than ten amino acids (aa). Moreover, 

5. **Categorization:**
   We categorized the ORFs  into five groups based on their presence in the tested genomes: 
   * found in all tested genomes category.
   * found in all pathogenic category.
   * found in all nonpathogenic category.
   * found in some pathogenic category.
   * found in some nonpathogenic genomes.

The following image presents the filtration and categorizing process.

![figure_19_upscaled](https://github.com/Fatomk11295/ORFs_comparative_analysis/blob/main/images/figure_19_upscaled%20(1).png).
