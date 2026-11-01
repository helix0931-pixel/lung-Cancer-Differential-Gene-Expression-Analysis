# lung-Cancer-Differential-Gene-Expression-Analysis
Lung Cancer Differential Gene Expression Analysis
A Python-based bioinformatics project comparing lung adenocarcinoma and normal lung tissue using the public GEO dataset GSE10072.
Status: Analysis workflow scaffold. Add the executed notebook, final volcano plot, and verified result counts before describing the analysis as fully reproducible.

Project overview
This project demonstrates a differential gene-expression workflow using normalized Affymetrix microarray data:
1. Retrieve the GEO series matrix and sample metadata.
2. Map platform probe identifiers to gene symbols using GPL96 annotation.
3. Summarize multiple probes per gene (the current learning workflow uses the mean).
4. Compare tumor and normal samples using Welch's two-sample t-test.
5. Adjust p-values using the Benjamini–Hochberg false discovery rate procedure.
6. Classify genes using predefined effect-size and adjusted-p-value thresholds.
7. Visualize the results with a volcano plot.
Dataset
- GEO accession: GSE10072
- Platform: GPL96 – Affymetrix Human Genome U133A
- Organism: Homo sapiens
- Data type: Microarray expression data (RMA-normalized, log2 scale in the series matrix)
Check the GEO sample annotations in the downloaded series matrix rather than relying on hard-coded title strings. Confirm the actual group sizes and sample identities in the notebook before analysis.
Repository layout
lung-cancer-dge/
├── README.md
├── requirements.txt
├── .gitignore
├── notebooks/
│   ├── README.md
│   └── lung_cancer_dge.ipynb       # Add your executed Colab notebook
├── data/
│   ├── README.md
│   ├── raw/                        # Downloaded GEO files (not committed)
│   └── processed/                  # Processed matrices (not committed)
├── results/
│   ├── README.md
│   ├── figures/                    # Volcano plot and other figures
│   └── tables/                     # Differential-expression result tables
└── src/
    └── README.md                   # Optional reusable Python functions
Run the analysis
Option A: Google Colab
1. Open Google Colab.
2. Upload or open notebooks/lung_cancer_dge.ipynb.
3. Run the notebook cells from top to bottom.
4. Confirm that the tumor and normal sample groups were correctly identified.
5. Save the executed notebook and export the volcano plot and results table into results/.
Option B: Local Python environment
python -m venv .venv
Activate the environment, then install dependencies:
pip install -r requirements.txt
The current workflow was developed for Colab. You may need to adapt file paths for local execution.
Statistical approach
The GEO series matrix contains log2-scale expression values. For each gene:

Log2 fold change
log2FC = mean(tumor expression) - mean(normal expression)
Fold change
fold_change = 2 ** log2FC
Statistical test: Welch's independent two-sample t-test.

Multiple-testing correction: Benjamini–Hochberg (BH) FDR.

Illustrative classification thresholds:
Classification	Criteria
Upregulated	log2FC >= 1 and adjusted p-value < 0.05
Downregulated	log2FC <= -1 and adjusted p-value < 0.05
Not significant	Does not meet either definition


These are analysis thresholds, not universal biological cutoffs.
Outputs to add
After running the notebook, save:
- results/figures/volcano_plot.png
- results/tables/differential_expression_results.csv
- results/tables/significant_genes.csv
Update the Results section below with the actual values produced by your run. Do not invent or estimate result counts.
Results
Not yet populated. Add the actual number of tested genes, significant genes, upregulated genes, and downregulated genes after running the notebook.
Important limitations
- This is microarray data, not raw RNA-seq count data. Do not apply RNA-seq count-based methods directly to these normalized intensities.
- Welch's t-test treats the two groups as independent. If the study design includes matched tumor-normal samples, a paired or design-aware model may be more appropriate.
- Averaging probes mapped to the same gene is a simplifying choice. Probe quality, multiple mappings, and annotation version can affect results.
- Confirm sample labels and group sizes from GEO metadata before interpreting findings.
- Treat this as an educational/exploratory analysis. Validate findings with an appropriate model and independent data before making biological or clinical claims.
Skills demonstrated
- Python data handling with pandas and NumPy
- Retrieval and preprocessing of public GEO data
- Microarray probe annotation
- Differential expression testing
- Multiple hypothesis correction and FDR
- Volcano plot visualization
- Reproducible project organization
References
- GSE10072 – NCBI GEO
- GPL96 – NCBI GEO
- SciPy statistics
- Statsmodels
