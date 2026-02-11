# DKD scRNA-seq Analysis Pipeline (GSE279086)

Complete workflow for **40 kidney samples** (DKD vs healthy) from NCBI GEO GSE279086. **R + Python**.

## 🧬 Workflow (4 Files)
01_seurat.Rmd → Create object + initial QC + UMAP
02_qc_umap.Rmd → Deep QC + filtering + Harmony clustering
03_python.Rmd → h5AD conversion + CellTypist annotation
04_deg_pathway.Rmd → DEG analysis + Reactome GSEA

## 📊 Key Results
Total: 15k cells → Post-QC: 12k retained (83%)
Clusters: 23 cell types (Harmony + CellTypist)
Top DEGs: PC, MT-ATP6 highly upregulated in DKD

## 🚀 Quick Start
```bash
renv::restore()
Rscript -e "rmarkdown::render('analysis/01_seurat.Rmd')"
