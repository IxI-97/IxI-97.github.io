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

 <div align="center">
    <img src="https://github.com/IxI-97/IxI-97.github.io/blob/main/disegno.svg?raw=true">
</div>

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

 <div align="center">
    <img src="https://github.com/IxI-97/IxI-97.github.io/blob/main/MOFA2.svg?raw=true">
</div>