# BiomiX Tutorial

## Introduction

The usage of high-throughput technology in health and biological sciences boosted the amount of information obtainable from samples. The increased dependency on these technologies revealed how data analysis represents the bottleneck step in both time and in bioinformatics skilled users. BiomiX tool offers an efficient and time-saving pipeline to analyze -omics data singularly and integrate multi-omics data from the same patients or samples. 

BiomiX was developed from the European PRECISESADS database, including overlapping data of whole blood and sorted immune cells, transcriptomics, plasma and urine metabolomics, and whole blood methylomics from 363 SLE patients and 508 controls (CTRLs). Transcriptomics are analysed through a differential gene expression (DGE) analysis using Deseq package, and metabolomics peaks changes were quantified and statistically tested. Peaks annotation are performed automatically by comparing m/z, retention time and spectra stored in public databases (HMDB, MoNA, Massbank, KEGG, Ceu Mass Mediator). Methylomics analysis are performed by ChAMP R package. Common sources of variations among the -omics was identified by Multi-Omics Factor Analysis (MOFA) integration. 

BiomiX carries out the analysis highlighting the most important features for each -omics, including its log2FC, adjusted p-value, heatmaps and volcano plots. Furthermore, transcriptomics data analysis produces output ready for EnrichR and GSEA tools, to ease the exploration of biological processes changes. The user can insert a panel of genes used by BiomiX to define subgroups of patients to compare to the control group, as already done in our previous publications on SLE IFN-α positive patients in PRECISESADS data using a panel of 26 IFN-α genes. Metabolomics analysis and annotation have been made automatized and accessible, without technical and bioinformatic knowledge. MOFA integration has been automatized to catch group differences while factors interpretability has been implemented, providing articles, biological pathways and clinical data of each relevant MOFA factor. The reliability of the tool is based on the well-tested pipeline and algorithms that are included in it. The synergy of these methods highlights a comprehensive multiomics view required to characterize SLE inflammatory environment and other patients’ conditions

This user-friendly tool, based on R is compatible for Linux and Microsoft OS, and aim to make accessible the multiomics analysis to users not expert in bioinformatics.

- Go to [Installation page](Installation.md)
- Go to [Single-omics analysis page](Single-omics_analysis.md)
- Go to [Integration analysis page](Integration_analysis.md)


![alt text](https://github.com/IxI-97/IxI-97.github.io/blob/main/BiomiX_visual4.png?raw=true)

![alt text](https://github.com/IxI-97/IxI-97.github.io/blob/main/BiomiX_visual2.png?raw=true)
