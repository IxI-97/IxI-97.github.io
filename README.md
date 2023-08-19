# BiomiX Tutorial

## Introduction

The usage of high-throughput technology in health and biological sciences boosted the amount of information obtainable from samples. The increased dependency on these technologies revealed how data analysis represents the bottleneck step in both time and in bioinformatics skilled users. BiomiX tool offers an efficient and time-saving pipeline to analyze -omics data singularly and integrate multi-omics data from the same patients or samples. 

BiomiX was developed from the European PRECISESADS database, including overlapping data of whole blood and sorted immune cells, transcriptomics, plasma and urine metabolomics, and whole blood methylomics from 363 SLE patients and 508 controls (CTRLs). Transcriptomics are analysed through a differential gene expression (DGE) analysis using Deseq package, and metabolomics peaks changes were quantified and statistically tested. Peaks annotation are performed automatically by comparing m/z, retention time and spectra stored in public databases (HMDB, MoNA, Massbank, KEGG, Ceu Mass Mediator). Methylomics analysis are performed by ChAMP R package. Common sources of variations among the -omics was identified by Multi-Omics Factor Analysis (MOFA) integration. 

BiomiX carries out the analysis highlighting the most important features for each -omics, including its log2FC, adjusted p-value, heatmaps and volcano plots. Furthermore, transcriptomics data analysis produces output ready for EnrichR and GSEA tools, to ease the exploration of biological processes changes. The user can insert a panel of genes used by BiomiX to define subgroups of patients to compare to the control group, as already done in our previous publications on SLE IFN-α positive patients in PRECISESADS data using a panel of 26 IFN-α genes. Metabolomics analysis and annotation have been made automatized and accessible, without technical and bioinformatic knowledge. MOFA integration has been automatized to catch group differences while factors interpretability has been implemented, providing articles, biological pathways and clinical data of each relevant MOFA factor. The reliability of the tool is based on the well-tested pipeline and algorithms that are included in it. The synergy of these methods highlights a comprehensive multiomics view required to characterize SLE inflammatory environment and other patients’ conditions

This user-friendly tool, based on R is compatible for Linux and Microsoft OS, and aim to make accessible the multiomics analysis to users not expert in bioinformatics.

![alt text](https://github.com/IxI-97/IxI-97.github.io/blob/main/BiomiX_visual4.png?raw=true)

![alt text](https://github.com/IxI-97/IxI-97.github.io/blob/main/BiomiX_visual2.png?raw=true)

## Installation
### Linux OS
  1. Download Biomix from the github page and decompress it. The installation in the home directory is suggested. From bash type
```
  cd
  wget linktothelatestBiomiXversion
  tar -xvzf Biomix1.5.tar.gz
```
  2. BiomiX uses conda to install the r and python package dependencies. 
  Install conda from the website: https://docs.conda.io/en/latest/miniconda.html or type on the bash 
```
  wget https://repo.anaconda.com/miniconda/Miniconda3-py310_23.3.1-0-Linux-x86_64.sh
  bash Miniconda3-py310_23.3.1-0-Linux-x86_64.sh
```
  3. Follow the instructions, selecting conda init = yes. Close and reopen the bash terminal.

  4. Create your BiomiX environment (BiomiX-env) in conda typing on the bash
```
  conda create -n BiomiX-env python=3.9 r-base=4.2.0 r-essentials
```
  5. Activate your BiomiX environment
```
  conda activate BiomiX-env
```
  6. Run the BiomiX_INSTALL Python script
```
  python3 path/to/BiomiX1.7/_INSTALL/BiomiX_INSTALL.py
```
  7. Enjoy BiomiX!


### Windows OS
  1. Download Biomix from the github page and decompress it (by application e.i Winzip or terminal cmd). The installation in the home directory is suggest.
     If using the windows terminal type
```
  cd
  wget linktothelatestBiomiXversion
  tar -xvzf Biomix1.5.tar.gz
```
  2. BiomiX uses conda to install the r and python package dependencies. 
  Install conda from the website https://docs.conda.io/en/latest/miniconda.html

  3. Follow the installation instructions
  
  4. Open the search in Windows taskbar the application "Anaconda powershell prompt"

  5. Create your BiomiX environment (BiomiX-env) in conda typing on the conda powershell
```
  conda create -n BiomiX-env python=3.9
```
  6. Activate your BiomiX environment
```
  conda activate BiomiX-env
```
  7. Install R and igraph package.
```
  conda install -c conda-forge r-base=4.1.3
```
  8. Run the BiomiX_INSTALL Python script clicking on it or typing in the conda powershell
```
  python path/to/BiomiX1.5/_INSTALL/BiomiX_INSTALL.py
```
  9. Enjoy BiomiX!

### Troubleshooting
#### **ModuleNotFoundError: No module named 'package name'** 
It happens during the conda installation "step 2" because the python installed in your computer doesn't have. Can be fixed typing in the terminal: **pip install 'package name'**
  
## Single-omics analysis
### Transcriptomics

BiomiX analyses the expression matrix to quantify the expression difference between two groups of samples discriminating automatically between raw counts, analyzed using the Deseq package, and normalized counts, analyzed by Limma package. Biomix requires an expression matrix **Msg** where the columns **s** represent the samples while the rows **g** contain the genes in Ensembl or gene names format. The analysis highlights the differentially expressed genes (DEG), their Log2FC and p.adj plus pff reports containing volcano plots, heatmaps and gene variances. If sex and gender are available in the metadata these will be automatically used to correct the Deseq2 or Limma model. The default thresholds to consider the differentially expressed genes were set to Log2FC > 0.5 and p.adj < 0.05. The p.value has been adjusted using the False Discovery Rate (FDR) method. The enrichment of biological process in the results is explored in the R version of EnrichR. Moreover, pre-treated output files are produced to carry out the gene set enrichment analysis using GSEA or EnrichR. The expression matrix is also normalizalized by variance stabilizing transformation (vst) for data visualization and MOFA integration

  - **Additional features**
    
    - **Gene Panel subgrouping**: It is possible to provide a panel of genes within *GENE_PANEL* file, in *Transcriptomics/INPUT* directory. The genes must be in Gene symbol format and tab-delimited (by enter button). 

  ```
GENES_FOR_SUBPOPULATION
SIGLEC1
IFIT3
IFI6
LY6E
MX1
USP18
OAS3
IFI44L
  ```
  - These genes will build a heatmap containing the expression standard deviation of each specific gene in each sample. This will allow 
   us to classify the condition/disease samples in positive and negative while BiomiX will carry out a differential gene expression 
   analysis comparing the chosen controls and these two groups.
    - **Subgrouping comparison with other clinical/biological data**: It is possible to add a column named **MARKER** in the metadata containing the classification according to clinical or biological analysis on the samples. This marker can be compared to the subgrouping obtained from the user gene panel to observe similarities or differences.

  - - ![alt text](https://github.com/IxI-97/IxI-97.github.io/blob/main/Heatmap_BLymphocytes_CTRL_vs_SLE2.svg?raw=true)
  - - **EnrichR**: It is possible to copy the gene list provided in the results to obtain the enrichment of the biological pathways direct in EnrichR webtool: https://maayanlab.cloud/Enrichr/.
  ![alt text](https://github.com/IxI-97/IxI-97.github.io/blob/main/enrichR.svg?raw=true)
    - **GSEA**: It is possible to upload the gene matrix and the metadata information pre-processed by BiomiX to run a GSEA analysis: https://www.gsea-msigdb.org/gsea/index.jsp.
  ![alt text](https://github.com/IxI-97/IxI-97.github.io/blob/main/GSEA2.svg?raw=true)

TEST Go to [about page](about.md)

### Metabolomics

BiomiX metabolomics data requires peaks signals matrix **Msg** where the columns **s** represent the samples while the rows **g** contain the arbitrary peak numbers. BiomiX is flexible, allowing annotated and not annotated metabolomics data. If the
annotation is required, based on the available information can execute an MS1 annotation
(mass/charge ratio and retention time values required) or an MS2 one (fragmentation files . Mzml
required). If you have only row .mzML files, to generate the peak signals matrix we strongly suggest this easy R pipeline by
Á. Fernández-Ochoa (ADD THE TUTORIAL). 

The peak signals from the condition/treated
samples are compared with the CTRL calculating the Log2FC as the log2 of the ratio between the
median peak signal in condition-treated samples/ median peak signal in CTRL for each peak. The
p.value was evaluated by the non-parametric Mann-Whitney test and corrected through the FDR
method. Then, peaks are annotated using the Ceu Mass Mediator tool through the CMMR R
package, which provides a direct Application Programming Interface in R. To filter metabolites
contemporary associated with one identical peak, are automatically examined lists containing earlier
identified or predicted metabolites within the Human Metabolome Database (HMDB)31 These
include plasma, urine, saliva, cerebrospinal fluid, feces, sweat, breast milk, bile and amniotic fluid
samples. If MS/MS spectra are also available, a metabolite annotation of level two is possible.
BiomiX will automatically upload all the .Mzml file available in the indicated directory and verify
the peaks fragmentation spectra looking for a match in the MONA, MassBank, and HMDB.The user has to define a priority among these databases, where the first will be used as the reference while the others will fill the peaks not annotated by the higher priority database. The priority and the usage and not usage of these databases are fully customizable. The spectra predicted and the
ones retrieved in the. Mzml files are saved in the output folder. Each peak annotation detected in the
MS2 will automatically replace one obtained in MS1.

The significant metabolites increased and reduced are displayed in a volcano plot while a
logarithmic transformation is applied to the peak signal matrix for MOFA integration. To unveil the
change in biological pathways, BiomiX automatically exploits a methPath v1.0.5 from tidymass
v1.0.8 to spot enrichment in the metabolic process among the significantly changed metabolites.
Moreover, for a deeper analysis, it prepares ready-to-copy files as input for Metaboanalyst32. It is
one of the most advanced online tools for metabolomics analysis, including enrichment and
Metabolite set enrichment analysis. Autonomously, if transcriptomics results are available in
BiomiX analysis will join the metabolomics and transcriptomics results into files copiable on
Metaboanalyst to launch joint pathway analysis and network analysis.

### Methylomics

Biomix requires an expression matrix Msg where the columns s represent the samples while the rows g contain the CpG island annotation. The matrix must contain the beta-values, if not available, these can be obtained by the minfi R package33. The
Differential methylation analysis (DMA) is performed using the ChAMP database, providing the
results of the CpG island hypermethylated and hypomethylated with a volcano plot. The threshold
has been set as default to the beta value change (Δbeta) > |0.15| and p.adj < 0.05.

### MOFA integration
### MOFA factors interpretation
