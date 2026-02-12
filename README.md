# DKD scRNA-seq Analysis Pipeline (GSE279086)

Complete workflow for **40 kidney samples** (DKD vs healthy) from NCBI GEO GSE279086 using **Bash, R , Python**.

**LC** = Lean Control (healthy) | **T1D** = Type 1 Diabetes (DKD)


## 📊 Quality Control & Filtering

### Cell Quality Filtering
- min.features = 200  # Exclude empty/low-quality droplets
- min.cells = 3       # Retain informative genes only
- max.features = 7000 # Remove doublets/multiplets

**Rationale**: Standard thresholds eliminate noise while preserving biology [Seurat v5].

### QC Metrics
- percent.mt < 15%  # Exclude dying/apoptotic cells
- percent.rb < 20%  # Exclude stressed cells

**Mahalanobis distance < 0.95**: Removes top 5% multivariate outliers.

### Gene Filtering
- Keep protein-coding genes only

Focuses on functional genes, removes non-coding noise.

## 🔬 Data Processing Pipeline

### Normalization & Scaling
- SCTransform() + log-normalization

Stabilizes variance across expression levels for visualization/clustering.

### Feature Selection
- FindVariableFeatures(top 2500 HVGs)

Captures biological signal, reduces technical noise.

### Dimensionality Reduction
- PCA (1:100 dims) → Elbow plot → UMAP (2D)


## 🏷️ Cell Type Annotation
CellTypist(kidney_reference, p_thres = 0.5)

- Human adult kidney reference model
- Majority voting + probability threshold ≥0.5 for confident classification

## 🎯 Differential Expression Analysis
`FindAllMarkers(
test.use = "wilcox",
min.pct = 0.25, # ≥25% cells in either cluster
logfc.threshold = 0.25, # Biologically meaningful change
min.cells = 20, # Computational efficiency
only.pos = TRUE # Positive markers only
)`


**Wilcoxon rank-sum**: Gold standard for scRNA-seq DE testing.

## 🛤️ Pathway Enrichment
- ReactomeGSEA(Entrez IDs + human annotation)

Identifies dysregulated pathways in disease clusters.




## 📊 Key Results

- **Total**: 1,81,842 → 6,327 cells retained (QC)
- **Clusters**: 23 cell types (Harmony + CellTypist)  
- **T1D**: ↑PC/M-TAL markers, ↓EC-GC/C-TAL (tubular remodeling)


## 🚀 Quick Start
```bash
renv::restore()
Rscript -e "rmarkdown::render('analysis/01_seurat.Rmd')"
