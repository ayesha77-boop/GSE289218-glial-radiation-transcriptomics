# 🧠 GSE289218 — Glial Cell Transcriptomic Response to Radiation

A bioinformatics analysis of the **GSE289218** dataset from NCBI GEO, investigating differential gene expression in **Microglia** and **Astrocytes** following radiation exposure at two time points: **72 hours** and **2 weeks** post-treatment versus control.

> 📂 Dataset: [GSE289218 on NCBI GEO](https://www.ncbi.nlm.nih.gov/geo/query/acc.cgi?acc=GSE289218)

---

## 🔬 Biological Context

This project analyses transcriptomic changes in glial cells (microglia and astrocytes) in response to radiation. The two time points capture both acute (72hr) and longer-term (2wk) transcriptional responses, enabling a temporal comparison of gene regulation in the irradiated brain microenvironment.

| Comparison | Description |
|---|---|
| 72hr vs Control | Acute radiation response |
| 2wk vs Control | Sub-chronic radiation response |
| Cell Types | Microglia, Astrocytes |

---

## 📁 Project Structure

```
├── GSE_289218_geodataset.ipynb       # Main analysis notebook (Google Colab)
├── 72hr_vs_Control.csv               # DEG results — 72hr timepoint
├── 2wk_vs_Control.csv                # DEG results — 2wk timepoint
├── DEG_Microglia_72hr_vs_Control.csv
├── DEG_Microglia_2wk_vs_Control.csv
├── DEG_Astrocyte_72hr_vs_Control.csv
├── DEG_Astrocyte_2wk_vs_Control.csv
├── metadata.csv                      # Sample metadata
├── umap_coords.csv                   # Precomputed UMAP coordinates
├── pca_coords.csv                    # Precomputed PCA coordinates
└── README.md
```

---

## 🔍 Analysis Workflow

### 1. Environment Setup
- R 4.6.0 via `rpy2` for R–Python interoperability
- R packages: `ggplot2`, `ggrepel`, `readr`
- Python packages: `pandas`, `numpy`, `matplotlib`, `seaborn`, `scikit-learn`, `umap-learn`, `gseapy`, `adjustText`

### 2. Differential Gene Expression (DEG) Analysis
- Loaded DESeq2-derived results for each cell type × timepoint combination
- Renamed columns to standardised format (`log2FC`, `pval`, `padj`)
- Applied significance thresholds:
  - |log2FC| > 1.0
  - Adjusted p-value (padj) < 0.05
- Classified genes as **Up Regulated**, **Down Regulated**, or **Not Significant**

### 3. Dimensionality Reduction & Visualisation
- **UMAP** — coloured by cell type and condition; split-panel view per cell type
- **PCA** — full dataset and glial-cell-only subset (Microglia + Astrocyte)
- All plots saved as high-resolution `.png` files

### 4. Volcano Plots
- Cell-type-specific volcano plots for each comparison
- Top DEGs labelled with gene names using `adjustText` for non-overlapping annotation
- Colour-coded by regulation status

### 5. Heatmaps
- Heatmap of top DEGs per cell type across conditions
- Seaborn `clustermap` with hierarchical clustering

### 6. Pathway Enrichment Analysis
- Gene Set Enrichment Analysis via `gseapy`
- Enrichment run for each cell type at each timepoint
- Pathway comparison plots for 72hr and 2wk responses side-by-side

### 7. DEG Overlap Analysis
- Venn-style overlap comparison of DEGs between timepoints
- `DEG_Overlap_Comparison.png` generated to visualise shared vs unique gene sets

---

## 📊 Output Files Generated

| File | Description |
|---|---|
| `UMAP_CellType_Condition.png` | UMAP coloured by cell type and condition |
| `UMAP_Split_CellType_Condition.png` | Split UMAP panels per cell type |
| `PCA_CellType_Condition.png` | PCA of all samples |
| `PCA_GlialCells_Only.png` | PCA restricted to Microglia & Astrocytes |
| `Volcano_CellType_Specific.png` | Volcano plots per cell type |
| `Heatmap_CellType_DEGs.png` | DEG heatmap with clustering |
| `Enrichment_*.png` | Pathway enrichment plots (up to 8) |
| `Pathway_Comparison_72hr.png` | Pathway comparison at 72hr |
| `Pathway_Comparison_2wk.png` | Pathway comparison at 2wk |
| `DEG_Overlap_Comparison.png` | Overlap of DEGs between timepoints |

---

## 🛠️ Tech Stack

- **Python 3.12** — core analysis
- **R 4.6.0** (via `rpy2`) — DESeq2 output processing, R-based visualisations
- `pandas`, `numpy` — data wrangling
- `matplotlib`, `seaborn` — visualisation
- `scikit-learn` — PCA
- `umap-learn` — UMAP dimensionality reduction
- `gseapy` — pathway enrichment analysis
- `adjustText` — non-overlapping gene label placement
- **Google Colab** — development environment

---

## 🚀 Getting Started

```bash
# Clone the repository
git clone https://github.com/your-username/gse289218-glial-radiation-transcriptomics.git
cd gse289218-glial-radiation-transcriptomics

# Install Python dependencies
pip install pandas numpy matplotlib seaborn scikit-learn umap-learn gseapy adjustText rpy2

# Install R dependencies (inside R or via rpy2)
# install.packages(c("ggplot2", "ggrepel", "readr"))

# Open the notebook
jupyter notebook GSE_289218_geodataset.ipynb
```

> **Note:** DEG input files (`72hr_vs_Control.csv`, `2wk_vs_Control.csv`, cell-type-specific CSVs, `metadata.csv`, `umap_coords.csv`, `pca_coords.csv`) must be present in the working directory. These are derived from upstream DESeq2/Seurat processing of the GEO dataset.

---

## 📌 Dataset Reference

**GSE289218** — available on NCBI Gene Expression Omnibus (GEO):  
🔗 https://www.ncbi.nlm.nih.gov/geo/query/acc.cgi?acc=GSE289218

---

## 👩‍💻 Author

**Ayesha**  
Bioinformatics Project — GEO Dataset Analysis
