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

![alt text](https://github.com/IxI-97/IxI-97.github.io/blob/main/Metabolomics2.svg?raw=true)

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

MOFA was used according to the webpage developer indications
(https://biofam.github.io/MOFA2/) with normalized input data and reduced feature size. The
transcriptome data are normalized by the Variance Stabilising Transformation (VST) function in R
to make the data approximately homoskedastic. The top 5000 genes with higher variance in
normalized data are selected for the MOFA integration. The metabolomics data were transformed in
the pipeline using a log function to improve their Gaussian distribution. All peaks are used in the
analysis. The methylomics data didn't undergo any transformation, but like transcriptomics, only the
top 5000 CpG islands with higher variance were selected for the integration. MOFA can calculate
any desired total number of factors to explain the shared variance between the -omics datasets.
Other parameters, customizable in the interface, include Convergence mode, freqELBO, and
maxiter. Our implementation of MOFA included an automatized optimization of the total number of
factors. It runs the MOFA algorithm with an increasing number of factors, stopping the iteration
when at least three models showed the last MOFA factor explaining less than 1% of the variability
of the data. Only the top 3 models in separating our two conditions are maintained. For each
calculated factor in each model is determined how it can discriminate statistically between the two
groups. A non-parametric Mann-Whitney test tests the factor value distribution between the two
groups of samples correcting the p.values through the FDR method. The models selected are the
ones with the higher number of discriminating MOFA factors, and later comparing the p.adj values.

### MOFA factors interpretation

Both automatic and not automatic MOFA analysis
includes three methods to ease the user interpretation of the discriminating MOFA factors.
Correlation analysis. Users can upload a matrix containing binary or numerical clinical features to
integrate into the MOFA model. The numerical data are correlated through a Pearson correlation.
The binary clinical data are analysed using the Wilcoxon test after dividing the groups into positive
or negative categories. The nominal p.values were corrected using the Benjamini-Hochberg method.
Pathway analysis. BiomiX retrieves the top contributing genes, metabolites and CpG island for
discriminating factors in each MOFA model. Depending on the type of omics data is selected an R
package to highlight if there is an enrichment of some biological or metabolic pathway within the
enriched genes, metabolites and CpG island. The genes are analysed by EnrichR using the
"Reactome", "GO biological process" and "CODE and ChEA consensus TFs from ChIP-X"
libraries, while the metabolites are analysed through MetPath using the KEGG and HMDB
databases. The CpG islands are associated with their genes, if it exists and is examined through
EnrichR.
Pubmed bibliography research. Pubmed bibliography research. For each discriminating factor in
each MOFA model, the top contributing genes, metabolites and CpG island genes are used as input
in Pubmed research. The aim is to retrieve articles' abstracts associated with each discriminating
factor, to have each of them clues behind their identity. The search algorithm has three levels of
research, where the results merging more multiomics contributors are selected. At first, the algorithm selects the top 10 contributors from each omic provided as input and carries out research
in which only the article abstracts show at least one out of ten contributors for each omic in the text.
The second level does the same, but it selects article abstracts containing at least one out of ten
contributors in omics pairs (e.g. transcriptomics-metabolomics and methylomics-transcriptomics,
metabolomics-methylomics). Finally, the last-level research article abstracts show at least one out
of ten contributors within a single omics in the text. The output document includes, for each of
these three levels, an Excel document including the PubMed articles, the total number of matches
with the contributors and how many contributors are matched in the text. Furthermore, keywords,
DOI and the match information for each contributor are also available. The authors-provided
keywords are not optimal due to their absence in some journals. That is why BiomiX includes here
a further text mining analysis. The article's abstract spotted in each level is extracted and parsed
through the R lit search v 1.0.0 in a combination of 2-4 words. All the vocabularies generated by
each abstract are analysed to spot combinations of words more frequently. These words are filtered
by another vocabulary made up from gene set names as GO biological process (7751 gene sets) and
Human Phenotype Ontology (5405 gene sets). The most frequent 15 words are included in the
output Excel file. To conclude, the same analysis is repeated again, including all the abstracts
retrieved within the three-level.
