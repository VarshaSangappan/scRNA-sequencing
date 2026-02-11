# DKD scRNA-seq Analysis Pipeline (GSE279086)

Complete workflow for **40 kidney samples** (DKD vs healthy) from NCBI GEO GSE279086. **R + Python**.

**LC** = Lean Control (healthy) | **T1D** = Type 1 Diabetes (DKD)

## 🧬 Workflow (4 Files)
- `01_seurat.Rmd` - Create Seurat object 
- `02_qc_umap.Rmd` -  QC + filtering + umap + Harmony clustering
- `03_python.Rmd` - CellTypist annotation + majority voting
- `04_deg_pathway.Rmd` - DEG analysis + Reactome GSEA

## 📊 Key Results
Total:     15k → 12k cells retained (83%)
Clusters:  23 cell types (Harmony + CellTypist)
T1D:       ↑PC/M-TAL markers, ↓EC-GC/C-TAL (tubular remodeling)

## 🚀 Quick Start
```bash
renv::restore()
Rscript -e "rmarkdown::render('analysis/01_seurat.Rmd')"
