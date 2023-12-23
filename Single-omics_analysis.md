## Single-omics analysis
### Transcriptomics

#### Input information
BiomiX analyses expression matrixes to quantify the expression difference between two groups of samples. It can discriminate automatically between raw counts (analyzed by the Deseq package), and normalized counts (analyzed by the Limma package) requiring an expression matrix **Msg** where the columns **s** represent the samples while the rows **g** contain the genes in Ensembl or gene names format. To obtain the desired format BiomiX has a quick file modifier to easily lead the user to the right format. (Read more in the interface usage section)

BiomiX is developed to deconvolute matrices containing samples from different experiments and select only the ones the user wants to analyse (E.i analyse only B cells in a matrix containing the expression of B cells, T cells, Neutrophiles and Monocytes). This addition was developed to avoid the sorting of each group of samples in different matrices. The format to respect is clear, we suggest to call sample names using an ID number (e.i 3560087) for the analysis, except when there are multiple samples from the same patients, in this case, a single ID number is not enough. To distinguish these multiple samples the format suggested is ID number + tissue_name (e.i 3560087_BLymphocytes). 

The tool has been developed to accept both formats and to provide input in MOFA including only the ID number to allow integration with different omics. So if you have a convoluted matrix it is enough to run the DGE analysis, cross the selection option and use in the label the name of the tissue. BiomiX will look in the SAMPLE_TYPE column and filter on the tissue_name.

#### The analysis
The analysis highlights the differentially expressed genes (DEG), their Log2FC and p.adj plus pff reports containing volcano plots, heatmaps and gene variances. If sex and gender are available in the metadata these will be automatically used to correct the Deseq2 or Limma model. The default thresholds to consider the differentially expressed genes were set to Log2FC > 0.5 and p.adj < 0.05. The p.value has been adjusted using the False Discovery Rate (FDR) method. The enrichment of biological process in the results is explored in the R version of EnrichR. Moreover, pre-treated output files are produced to carry out the gene set enrichment analysis using GSEA or EnrichR. The expression matrix is also normalizalized by variance stabilizing transformation (vst) for data visualization and MOFA integration



<div align="center">
    <img src="https://github.com/IxI-97/IxI-97.github.io/blob/main/Transcriptomics.svg?raw=true">
</div>

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

<div align="center">
    <img src="https://github.com/IxI-97/IxI-97.github.io/blob/main/Heatmap_BLymphocytes_CTRL_vs_SLE2.svg?raw=true">
</div>

  - - **EnrichR**: It is possible to copy the gene list provided in the results to obtain the enrichment of the biological pathways direct in EnrichR webtool: https://maayanlab.cloud/Enrichr/.

<div align="center">
    <img src="https://github.com/IxI-97/IxI-97.github.io/blob/main/enrichR.svg?raw=true">
</div>

  - - **GSEA**: It is possible to upload the gene matrix and the metadata information pre-processed by BiomiX to run a GSEA analysis: https://www.gsea-msigdb.org/gsea/index.jsp.

 <div align="center">
    <img src="https://github.com/IxI-97/IxI-97.github.io/blob/main/GSEA2.svg?raw=true">
</div>

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

 <div align="center">
    <img src="https://github.com/IxI-97/IxI-97.github.io/blob/main/Metabolomics.svg?raw=true">
</div>

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

 <div align="center">
    <img src="https://github.com/IxI-97/IxI-97.github.io/blob/main/Methylomics.svg?raw=true">
</div>


### Interface usage
#### Assisted input modification
Click on the input button and select the file you want to modify. 


 <div align="center">
    <img src="https://github.com/IxI-97/IxI-97.github.io/blob/main/INPUT_1.png?raw=true">
</div>
 <div align="center">
    <img src="https://github.com/IxI-97/IxI-97.github.io/blob/main/INPUT_2.png?raw=true">
</div>


After the file selection, it is possible to decide if the selected file must be used as input for the analysis or if you desire to modify it in the BiomiX standard format.


 <div align="center">
    <img src="https://github.com/IxI-97/IxI-97.github.io/blob/main/INPUT_3.png?raw=true">
</div>


When you select "Yes" to the Pop-up "Do you want to modify the file?", another Pop-up will appear, asking for the file separator, the header, the column containing the ID and the type of decimal separator. 


 <div align="center">
    <img src="https://github.com/IxI-97/IxI-97.github.io/blob/main/INPUT_4.png?raw=true">
</div>


Then the matrix preview will appear in the "preview" tab, allowing the user to visualize if the format is the right one. If not the case it is possible to modify the table using the other tab, which contains buttons to remove specific columns and rows and eventually transpose the matrix. WARNING: The preview will include the first 10 columns and rows, so it does not represent the entire matrix. 


 <div align="center">
    <img src="https://github.com/IxI-97/IxI-97.github.io/blob/main/INPUT_5.png?raw=true">
</div>
 <div align="center">
    <img src="https://github.com/IxI-97/IxI-97.github.io/blob/main/INPUT_6.png?raw=true">
</div>
