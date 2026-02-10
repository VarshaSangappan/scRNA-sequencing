# DKD scRNA-seq Analysis Pipeline (GSE279086)

Complete single-cell RNA-seq workflow for **40 kidney samples** (DKD patients vs healthy controls) from NCBI GEO GSE279086. Uses **Seurat (R)** + **Scanpy (Python)** for QC, Harmony integration, CellTypist annotation, and GSEA pathway analysis.

## Workflow

flowchart 
    A[GSE279086<br/>40 kidney samples] --> B[Seurat Object<br/>QC Metrics]
    B --> C[QC Filter<br/>Violin Plots]
    C --> D[LogNorm + PCA<br/>2000 HVFs]
    D --> E[Harmony Integration]
    E --> F[UMAP + Clustering]
    F --> G[CellTypist Annotation]
    G --> H[DEG + GSEA]
    style A fill:#e1f5fe
    style H fill:#f3e5f5
