# Comparative analyses of Open Reading Frames (ORFs) between pathogenic and nonpathogenic Staphylococci species

# Introduction

This repository guides analyses in the publication "Identification of pathogenic-specific open reading frames in staphylococci species".

## Methodology :

   **1.** Extraction, filtration, and categorizing of ORFs

   **2.** Annotation

   **3.** Conservation test

   **4.** Function prediction

   **5.** Explore a candidate ORF

---

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

2. **Data Collection:**
   Download the whole genome sequence for the selected species from [NCBI's FTP server](https://ftp.ncbi.nlm.nih.gov). You can find full specifications about the WGS data for the selected species in this [file](https://docs.google.com/spreadsheets/d/1wd9hzx6mVgmB8F8CK_Etvh1MnovFnqct/edit?usp=sharing&ouid=103975173682819978105&rtpof=true&sd=true).

3. **ORF Extraction:**
   We employed the [EMBOSS getorf algorithm](https://www.bioinformatics.nl/cgi-bin/emboss/getorf) to extract ORFs from the selected genomes. We selected the optional qualifier **-find [1]** to identify the translation of ORFs in the regions between the start and stop codons.

Run getorf and extract ORFs from a specific genome on a Linux system using bash command

   ```bash
   getorf -sequence genome_1.fa -find 1 -outseq output.txt
   ```

4. **ORF Filtering:**
   Extracted ORFs were filtered based on size, discarding any ORF shorter than ten amino acids (aa). 

   ```python
   keep_orfs = []
   for orf in orfs_list:
      if len(orf) >= 10:
         keep_orfs.append(orf)
   ```
         
5. **Categorization:**
   We categorized the ORFs  into five groups based on their presence in the tested genomes: 
   * found in all tested genomes.
   * found in all pathogenic tested genomes.
   * found in all nonpathogenic tested genomes.
   * found in some pathogenic tested genomes.
   * found in some nonpathogenic tested genomes.

The following image presents the filtration and categorizing process.

![figure_1.jpg](https://github.com/Fatomk11295/ORFs_comparative_analysis/blob/main/images/figure_1.jpg)

---

### Annotation 

The functional annotation of ORFs followed two approaches: 

1. **Direct approach:**
   * Utilize annotated protein files from [GenBank and RefSeq databases](https://ftp.ncbi.nlm.nih.gov) 
   * Initiate annotation for all ORFs in each category using the direct approach.
   * The sequence and coordinate of each ORF matched with its resembled annotated protein of  the tested genomes.

2. **Indirect approach:**
   * For ORFs that failed in the direct annotation tested for the indirect annotation that utilized the BLAST tool. 
   * Rely on the traditional [BLASTp tool](https://blast.ncbi.nlm.nih.gov/Blast.cgi?CLIENT=web&DATABASE=nr&NCBI_GI=on&PAGE=Proteins&PROGRAM=blastp&QUERY=IDQILETNRIACRFNHSNQKYAFSITFQEECAHVTLVVYGRNLHKHFFYWKLHKQLIDLIANPNDMFFF&END_OF_HTTPGET=Y). 
   * The BLAST tool parameters were adjusted to search in the non-redundant protein sequence database for homologous sequences to ORFs only in the Staphylococcus organism (taxid 1279), targeting a maximum of 100 species. Both identity level and query coverage should be higher than 85%.

Following the annotation, perform gene enrichment analysis for ORFs in each category using the [Blast2GO tool](https://www.blast2go.com/). To identify significantly enriched biological processes in pathogenic tested genomes, we performed a two-tailed Fisher exact test provided by Blast2Go.

The ORFs whose functions were unknown and were not annotated through either approach will serve as the foundation for subsequent analysis. We have designated these as unknown ORFs (unORFs).

---

### Conservation test

The assessment of the conservation level of unknown ORFs (unORFs) unfolded in three sequential stages:

1. **Assessment within the Staphylococcus Genus:**
   - Evaluate the conservation of unORFs within the Staphylococcus genus.

2. **Specific Assessment within Pathogenic Staphylococci Species:**
   - Examine the conservation of unORFs specifically within pathogenic staphylococci species.

3. **Assessment Outside the Staphylococcus Genus:**
   - Investigate the conservation of unORFs beyond the Staphylococcus genus.

To execute these conservation tests, we employed the [tblastn tool](https://blast.ncbi.nlm.nih.gov/Blast.cgi?PROGRAM=tblastn&PAGE_TYPE=BlastSearch&LINK_LOC=blasthome), extracting data based on identity level and query coverage (set at >= 85).

For the determination of the pathogenicity score of each unORF, we utilized PathogenFinder 1.1 and NCBI Pathogen detection datasets (Cosentino et al., 2013; NCBI, 1988), classifying unORFs as either known to be pathogenic (1) or of unknown pathogenicity (0). The pathogenicity of an ORF is defined by the number of pathogenic genomes possessing a homologous sequence. The pathogen frequency of an ORF is specified by dividing the pathogenicity of an ORF by the total number of genomes, as illustrated in the following figure.

![figure_2.jpg](https://github.com/Fatomk11295/ORFs_comparative_analysis/blob/main/images/figure_2.jpg) 

The subsequent analysis will be grounded in the 23 unknown ORFs (unORFs) that exhibited remarkably high conservation within pathogenic staphylococci genomes, featuring a pathogen frequency of >= 0.98. This subset of 23 unORFs will be denoted as selected ORFs (selORFs).

---

### Function prediction

We predicted the function of the 23 selORFs through 3 stages:

   1. **Function Prediction Using DeepGoPlus Algorithm:**
      * Employed the [DeepGoPlus algorithm](https://deepgo.cbrc.kaust.edu.sa/deepgo/) for predicting the functions of the 23 selected ORFs (selORFs). This algorithm utilizes deep learning to extract features from query protein sequences and incorporates cross-species protein-protein interaction networks.

   2. **Ribosomal Binding Site (RBS) Motif Verification with Prodigal Algorithm:**
      * Utilized the [Prodigal (Prokaryotic gene recognition and translation initiation site identification) algorithm](http://compbio.ornl.gov/prodigal/) to identify ribosomal binding site (RBS) motifs in the S. aureus Mu3 genome. This step aimed to verify whether the RBS motif preceded the ORF or not.

   3. **Exploration of Neighboring Genes for Regulatory Functions:**
      * Explored the surrounding genes to test the hypothesis that the selected ORFs (selORFs) might be non-coding RNA, potentially translated on different frames, and possibly involved in regulatory functions. To explore the neighboring genes for each ORF and outline its precise locus, the interval between all selected ORFs (selORFs) and genes of the S. aureus Mu3 genome was measured per their coordinates. We downloaded the annotated protein file for S. aureus Mu3 from the [Genbank FTP website](https://ftp.ncbi.nlm.nih.gov/genbank/).
      * The full code for this assay can be found in this shared [python notebook](https://colab.research.google.com/drive/1CZ5nzGchY-NNEcuHAzCtOIcnrPiPS62f?usp=sharing).

---
### Explore a candidate ORF

We explored the candidate selORF with ID: AP009324.1_34709, which exhibited remarkable conservation in 102 of 200 pathogenic species and conservatively embedded within the 50S ribosomal L1 protein of several species. We employed [Clustal Omega- Multiple sequence alignment (MSA)](https://www.ebi.ac.uk/Tools/msa/clustalo/)  to assess the locus conservation assay within genomes closely related to the Staphylococcus genus. 

The genomes that were selected for this assay:
   1. Salinicoccus alkaliphilus DSM 16010 (NZ_FRCF01000009.1)
   2. Salinicoccus albus DSM 19776 strain YIM-Y21 (NZ_ARQJ01000028.1)
   3. Salinicoccus carnicancri Crm 50.SCCRM.1_10 (NZ_ANAM01000010.1)
   4. Nosocomiicoccus ampullae strain DSM 19163 (NZ_JACHHF010000004.1)
   5. Nosocomiicoccus massiliensis isolate MGYG-HGUT-01449 (NZ_CABKSY010000018.1)

Similarly, their genome and protein sequences were downloaded from [Genbank FTP website](https://ftp.ncbi.nlm.nih.gov/genbank/).

---

### Underlying data available at figshare open repository

**Citation:** Farhan, Fatima; Karlowski, Wojciech M.; Zielezinski, Andrzej (2023). Underlying data for ‘Identification of pathogenic-specific open reading frames in staphylococci species’. figshare. Dataset. https://doi.org/10.6084/m9.figshare.24588306.v1

---
### License

[CC BY 4.0](https://doi.org/10.6084/m9.figshare.24588696.v1)
