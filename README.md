# TCGA-LGG-GBM-Neuroinflammation
Differential expression analysis of neuroinflammation-associated genes in TCGA lower-grade glioma vs glioblastoma
# Neuroinflammation-Associated Gene Expression in TCGA LGG vs GBM

## Overview
This project compares the expression of ten neuroinflammation-associated 
genes between TCGA lower-grade glioma (LGG) and glioblastoma (GBM) primary 
tumor samples, using publicly available RNA-seq data. The analysis asks 
whether genes tied to inflammasome signaling and innate immune activity 
differ in expression across glioma grade.

## Key finding
Six of ten candidate genes (CXCL10, CASP1, PYCARD, IL18, AIF1, IL1B) showed 
significantly higher expression in GBM than LGG after multiple-testing 
correction, with CXCL10 showing the largest effect (Cliff's δ = 0.80, 
adjusted p = 3.8×10⁻⁵⁰). Notably, downstream inflammasome effector genes 
(CASP1, PYCARD, IL18, IL1B) were significantly elevated while the upstream 
sensor NLRP3 itself showed no significant difference — consistent with 
NLRP3 activity being regulated post-translationally rather than at the 
transcript level.

## Data source
TCGA GBMLGG cohort (TCGA.GBMLGG.sampleMap/HiSeqV2), accessed via UCSC Xena.
516 LGG and 154 GBM primary tumor samples.

## Methods
Two-sided Mann-Whitney U tests per gene, Benjamini-Hochberg correction 
across the 10-gene panel, Cliff's delta as effect size. Full details in 
the report.

## Contents
- `analysis.ipynb` — complete analysis code (Python, pandas/scipy/statsmodels)
- `report/` — full written report (PDF)
- `results/` — statistical results table (CSV)
- `figures/` — expression distribution figure (PNG)

## Limitations
Exploratory analysis of bulk-tumor expression data; does not establish 
causation, identify cellular source of expression signals, or demonstrate 
longitudinal tumor progression. See report for full discussion.

## Author
[Swasti Maurya] — Biological Sciences BS student, 
University at Buffalo
