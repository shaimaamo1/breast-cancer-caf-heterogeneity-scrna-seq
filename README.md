# Decoding Cancer-Associated Fibroblast Heterogeneity in the Breast Cancer Microenvironment Using Single-Cell RNA Sequencing

[![R](https://img.shields.io/badge/R-4.x-blue)](https://www.r-project.org/)
[![Seurat](https://img.shields.io/badge/Seurat-scRNA--seq-6A5ACD)](https://satijalab.org/seurat/)
[![Harmony](https://img.shields.io/badge/Harmony-Batch%20Correction-violet)]()
[![CellChat](https://img.shields.io/badge/CellChat-Cell--Cell%20Communication-teal)]()
[![Project](https://img.shields.io/badge/Project-Bioinformatics-green)]()
[![Status](https://img.shields.io/badge/Status-Completed-brightgreen)]()

## Project Summary

This project investigates **Cancer-Associated Fibroblast (CAF) heterogeneity** in the breast cancer tumor microenvironment using **single-cell RNA sequencing (scRNA-seq)** data. The workflow identifies major tumor microenvironment cell populations, extracts CAF populations, re-clusters CAFs, annotates CAF subtypes, and explores functional differences between CAF populations using differential expression and cell-cell communication analysis.

CAF populations are important components of the tumor microenvironment because they can contribute to extracellular matrix remodeling, inflammatory signaling, immune regulation, and tumor progression.

## Dataset

| Item | Description |
|---|---|
| Dataset | GSE176078 |
| Disease | Breast cancer |
| Data type | Single-cell RNA sequencing |
| Samples | 26 primary breast tumors |
| Subtypes | ER+, HER2+, and TNBC |
| Initial cells loaded | 100,064 cells |
| Cells retained after QC | 81,820 cells |
| Main tools | Seurat, Harmony, CellChat in R |

## Research Aim

To decode CAF heterogeneity in breast cancer and investigate CAF functional diversity through:

- Major cell-type annotation
- CAF isolation and re-clustering
- CAF subtype annotation
- Differential expression analysis
- Cell-cell communication analysis
- Biological interpretation of CAF-related signaling pathways

## Analysis Workflow

```text
Raw scRNA-seq matrix
        ↓
Create Seurat object
        ↓
Quality control and filtering
        ↓
Normalization and highly variable gene selection
        ↓
Scaling and PCA
        ↓
Harmony batch correction
        ↓
UMAP visualization and clustering
        ↓
Cluster marker identification
        ↓
Major cell type annotation
        ↓
CAF extraction
        ↓
CAF re-clustering
        ↓
CAF subtype annotation
        ↓
Differential expression analysis
        ↓
CellChat communication analysis
        ↓
Biological interpretation
```

## Methods

### 1. Quality Control and Filtering

Quality control was performed to remove low-quality cells and possible technical noise.

QC metrics included:

- `nFeature_RNA`
- `nCount_RNA`
- `percent.mito`

Filtering criteria:

- `nFeature_RNA > 300`
- `nFeature_RNA < 6000`
- `percent.mito < 10%`

After filtering, **81,820 cells** were retained from the original **100,064 cells**.

### 2. Normalization, PCA, Harmony, UMAP, and Clustering

Gene expression data were normalized using log normalization. Highly variable genes were selected, the data were scaled, PCA was performed, and Harmony was used for batch correction. UMAP visualization and graph-based clustering identified **12 transcriptionally distinct clusters**.

### 3. Differential Expression Analysis: TNBC vs ER+

Differential expression analysis was performed to compare gene expression patterns between **TNBC** and **ER+** cells.

Subtype-associated differentially expressed genes included:

- Higher in TNBC: `CYBA`, `PFN1`, `CORO1A`, `RAC2`
- Higher in ER+: `AGR3`, `MALAT1`

### 4. Major Cell-Type Annotation

Cluster-specific marker genes were identified using `FindAllMarkers()`. Canonical marker genes were used to annotate major cell populations in the tumor microenvironment.

Annotated cell populations included:

- T cells
- Epithelial cells
- Myeloid cells
- Endothelial cells
- CAFs
- Pericytes
- Plasma cells
- B cells
- Proliferating cells
- Basal epithelial cells
- pDCs
- Unknown cells

### 5. CAF Subsetting and Re-clustering

CAF populations were isolated from the annotated Seurat object and reanalyzed independently to investigate fibroblast heterogeneity in greater detail. CAF re-clustering revealed **5 transcriptionally distinct CAF populations**.

### 6. CAF Subtype Annotation

CAF subtypes were annotated using known CAF marker genes.

| CAF Subtype | Marker Genes |
|---|---|
| myCAF | ACTA2, TAGLN |
| iCAF | CXCL12, IL6 |
| matrixCAF | COL1A1, FN1 |
| apCAF | HLA-DRA, CD74 |
| proliferativeCAF | MKI67, TOP2A |

DotPlot and FeaturePlot visualizations were used to validate CAF subtype marker expression across re-clustered CAF populations.

### 7. Cell-Cell Communication Analysis Using CellChat

Cell-cell communication analysis was performed using **CellChat** to investigate signaling interactions between CAF subtypes.

The analysis included:

- Creating a CellChat object from the CAF dataset
- Loading the human CellChat ligand-receptor database
- Detecting overexpressed communication genes
- Identifying overexpressed ligand-receptor interactions
- Computing communication probabilities
- Aggregating signaling networks
- Interpreting pathway-level communication patterns

## Key Results

- The project identified major cell populations within the breast cancer tumor microenvironment.
- The initial dataset contained **100,064 cells**, and **81,820 cells** were retained after quality control.
- UMAP clustering identified **12 transcriptionally distinct clusters**.
- CAFs were isolated and re-clustered into **5 CAF subtypes**.
- CAF subtype annotation identified **myCAF**, **iCAF**, **matrixCAF**, **apCAF**, and **proliferativeCAF** populations.
- CellChat analysis revealed active communication between CAF subtypes.
- **COLLAGEN**, **MK**, and **FN1** signaling pathways showed strong information flow.
- **myCAF** and **apCAF** displayed stronger outgoing signaling activity compared with other CAF subtypes.

## Expected Outputs

| Output type | Examples |
|---|---|
| Quality control | Violin plots before and after filtering |
| Dimensionality reduction | PCA, UMAP, cluster UMAP |
| Annotation | Annotated UMAP, marker DotPlot, marker FeaturePlot |
| CAF analysis | CAF UMAP, CAF subtype UMAP, CAF marker tables |
| Differential expression | TNBC vs ER+ volcano plot and heatmap |
| Communication analysis | CellChat signaling network and pathway results |

## Important Marker Genes

| Cell population / CAF subtype | Marker genes |
|---|---|
| Epithelial / tumor cells | EPCAM, KRT8 |
| CAFs / fibroblasts | COL1A1, DCN |
| T cells | CD3D |
| B cells | MS4A1 |
| myCAF | ACTA2, TAGLN |
| iCAF | CXCL12, IL6 |
| matrixCAF | COL1A1, FN1 |
| apCAF | HLA-DRA, CD74 |
| proliferativeCAF | MKI67, TOP2A |

## Tools and Packages

- R
- Seurat
- Harmony
- CellChat
- ggplot2
- dplyr
- patchwork
- pheatmap

## Repository Structure

```text
breast-cancer-caf-heterogeneity-scrna-seq/
├── README.md
├── requirements.R
├── .gitignore
├── scripts/
│   └── scRNAseq_GSE176078_full_analysis.R
└── docs/
    └── project_notes.md
```

## Main Script

The main analysis workflow is available in:

```text
scripts/scRNAseq_GSE176078_full_analysis.R
```

## How to Run

### 1. Install packages

Open RStudio and run:

```r
source("requirements.R")
```

### 2. Prepare input data

Place the GSE176078 count matrix and metadata in a local folder. Raw sequencing data and large expression matrices are intentionally excluded from GitHub.

### 3. Edit the data path

Open the main script and update the data directory line according to your local file location.

### 4. Run the analysis

```r
source("scripts/scRNAseq_GSE176078_full_analysis.R")
```

## Notes

Raw sequencing data, large expression matrices, generated `.rds` files, and full output folders are intentionally excluded from GitHub. The repository focuses on the analysis code, documentation, and reproducibility instructions.

## Project Status

Completed as a bioinformatics course project focused on breast cancer tumor microenvironment analysis using single-cell RNA sequencing.

## Author

**Shaimaa Mohamed El Haddad**  
Biomedical Science Student | Computational Biology & Genomics Track
