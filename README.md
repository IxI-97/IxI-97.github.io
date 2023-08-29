# BiomiX Tutorial

## Introduction

The usage of high-throughput technology in health and biological sciences boosted the amount of information obtainable from samples. The increased dependency on these technologies revealed how data analysis represents the bottleneck step in both time and in bioinformatics skilled users. BiomiX tool offers an efficient and time-saving pipeline to analyze -omics data singularly and integrate multi-omics data from the same patients or samples. 

BiomiX was developed from the European PRECISESADS database, including overlapping data of whole blood and sorted immune cells, transcriptomics, plasma and urine metabolomics, and whole blood methylomics from 363 SLE patients and 508 controls (CTRLs). Transcriptomics are analysed through a differential gene expression (DGE) analysis using Deseq package, and metabolomics peaks changes were quantified and statistically tested. Peaks annotation are performed automatically by comparing m/z, retention time and spectra stored in public databases (HMDB, MoNA, Massbank, KEGG, Ceu Mass Mediator). Methylomics analysis are performed by ChAMP R package. Common sources of variations among the -omics was identified by Multi-Omics Factor Analysis (MOFA) integration. 

BiomiX carries out the analysis highlighting the most important features for each -omics, including its log2FC, adjusted p-value, heatmaps and volcano plots. Furthermore, transcriptomics data analysis produces output ready for EnrichR and GSEA tools, to ease the exploration of biological processes changes. The user can insert a panel of genes used by BiomiX to define subgroups of patients to compare to the control group, as already done in our previous publications on SLE IFN-α positive patients in PRECISESADS data using a panel of 26 IFN-α genes. Metabolomics analysis and annotation have been made automatized and accessible, without technical and bioinformatic knowledge. MOFA integration has been automatized to catch group differences while factors interpretability has been implemented, providing articles, biological pathways and clinical data of each relevant MOFA factor. The reliability of the tool is based on the well-tested pipeline and algorithms that are included in it. The synergy of these methods highlights a comprehensive multiomics view required to characterize SLE inflammatory environment and other patients’ conditions

This user-friendly tool, based on R is compatible for Linux and Microsoft OS, and aim to make accessible the multiomics analysis to users not expert in bioinformatics.

- Go to [Installation](Installation.md)
- Go to [Single-omics analysis guide](Single-omics_analysis.md)
- Go to [Integration analysis guide](Integration_analysis.md)


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

