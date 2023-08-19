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
