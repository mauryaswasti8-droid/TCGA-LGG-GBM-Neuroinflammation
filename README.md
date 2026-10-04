# TCGA-LGG-GBM-Neuroinflammation
Differential expression analysis of neuroinflammation-associated genes in TCGA lower-grade glioma vs glioblastoma
# Neuroinflammation-Associated Gene Expression in TCGA Lower-Grade Glioma and Glioblastoma

## Overview

This project investigates whether the expression of neuroinflammation-associated genes differs between two clinically and molecularly distinct glioma groups: lower-grade glioma (LGG) and glioblastoma (GBM). Using publicly available RNA-sequencing data from The Cancer Genome Atlas (TCGA), accessed through the UCSC Xena platform, this analysis compares expression levels of ten candidate genes spanning inflammasome signaling, cytokine pathways, and innate immune activity across 516 LGG and 154 GBM primary tumor samples.

**Research question:** How do expression patterns of selected neuroinflammation-associated genes differ between TCGA lower-grade glioma and glioblastoma primary tumor samples?

## Key Finding

Seven of ten candidate genes showed statistically significant expression differences between LGG and GBM after correction for multiple comparisons. Six genes (CXCL10, CASP1, PYCARD, IL18, AIF1, IL1B) had significantly higher median expression in GBM, while TLR4 had significantly lower expression in GBM. CXCL10 showed the largest effect (Cliff's delta = 0.798, adjusted p = 3.78 × 10⁻⁵⁰).

The most notable pattern emerges when comparing NLRP3 to its downstream pathway partners. NLRP3 itself, the inflammasome sensor, showed no statistically significant difference between tumor groups (adjusted p = 0.263). In contrast, CASP1, PYCARD, IL18, and IL1B, the genes NLRP3 recruits and activates downstream in the inflammasome cascade, were all significantly elevated in GBM. This dissociation is consistent with known inflammasome biology: NLRP3 activation is regulated primarily through post-translational mechanisms (priming and oligomerization) rather than through changes in transcript abundance, so its mRNA levels would not necessarily be expected to track pathway activity the way its downstream effectors do. The data suggest that inflammasome effector activity scales with glioma grade independently of NLRP3 transcriptional change.

## Data Source

- **Cohort:** TCGA Lower-Grade Glioma and Glioblastoma (GBMLGG)
- **Dataset:** `TCGA.GBMLGG.sampleMap/HiSeqV2`, accessed via [UCSC Xena](https://xenabrowser.net/datapages/?dataset=TCGA.GBMLGG.sampleMap%2FHiSeqV2&host=https%3A%2F%2Ftcga.xenahubs.net)
- **Expression unit:** log2(norm_count+1), as documented by Xena's dataset metadata
- **Samples analyzed:** 516 LGG and 154 GBM primary tumor samples (670 total), after excluding recurrent tumor and solid tissue normal samples from the full 702-sample cohort

## Candidate Genes

Ten genes associated with neuroinflammatory signaling were selected for this exploratory panel: NLRP3, PYCARD, CASP1, IL1B, IL18, TLR4, TNF, CXCL10, AIF1, and CSF1R. These span inflammasome assembly and activation (NLRP3, PYCARD, CASP1), downstream cytokine output (IL1B, IL18, TNF), innate immune sensing (TLR4), chemokine signaling (CXCL10), and myeloid/microglial cell markers (AIF1, CSF1R).

## Methods

For each candidate gene, expression values were compared between LGG and GBM samples using a two-sided Mann-Whitney U test. Resulting p-values were adjusted across the ten gene-level comparisons using the Benjamini-Hochberg procedure to control the false discovery rate. Cliff's delta was calculated as an effect size, oriented as GBM minus LGG, where positive values indicate a tendency toward higher expression in GBM and negative values indicate a tendency toward higher expression in LGG. An adjusted p-value below 0.05 was considered statistically significant. Analyses were performed in Python using SciPy for the Mann-Whitney U tests and statsmodels for multiple-testing correction. Full methodological detail, including software versions, is documented in the written report.

## Results Summary

| Gene | LGG median | GBM median | Cliff's δ | Adjusted p-value |
|---|---|---|---|---|
| CXCL10 | 3.243 | 7.635 | 0.798 | 3.78 × 10⁻⁵⁰ |
| CASP1 | 6.903 | 8.596 | 0.644 | 3.59 × 10⁻³³ |
| PYCARD | 6.967 | 8.183 | 0.582 | 1.83 × 10⁻²⁷ |
| IL18 | 7.088 | 8.250 | 0.470 | 2.12 × 10⁻¹⁸ |
| AIF1 | 9.033 | 9.904 | 0.382 | 1.27 × 10⁻¹² |
| IL1B | 6.142 | 7.441 | 0.357 | 2.72 × 10⁻¹¹ |
| TLR4 | 9.859 | 9.571 | -0.188 | 5.80 × 10⁻⁴ |
| TNF | 4.616 | 4.283 | -0.073 | 0.209 |
| NLRP3 | 7.090 | 7.040 | -0.063 | 0.263 |
| CSF1R | 11.563 | 11.663 | 0.037 | 0.488 |

Full statistical output, including raw p-values and sample counts, is available in `results/`.

## Limitations

This is an exploratory, cross-sectional comparison of bulk-tumor gene expression and should be interpreted accordingly:

- It compares two distinct tumor groups rather than following individual tumors over time, and therefore cannot demonstrate progression from LGG to GBM in the same patient.
- Bulk-tumor RNA-sequencing combines signal from tumor cells and all other cell types present in the tissue (immune cells, vasculature, stroma). Observed expression differences may reflect shifts in cellular composition rather than, or in addition to, changes in expression within a given cell type. This analysis cannot identify the cellular source of any observed signal.
- The statistical comparisons do not adjust for clinical or molecular covariates (age, IDH mutation status, treatment history) that are known to differ between LGG and GBM and could confound these associations.
- The ten genes analyzed were selected as a focused candidate panel based on known roles in inflammasome and innate immune signaling, not as a genome-wide or unbiased screen.
- Statistical significance does not, by itself, establish biological importance or causation.

## Repository Contents

- `TCGA_LGG_GBM_Analysis.ipynb`: Complete analysis code (Python: pandas, scipy, statsmodels, matplotlib), from raw data loading through final statistical results and figure generation.
- `report/`: Full written report covering background, methods, results, and discussion.
- `results/`: Statistical results table (CSV) with medians, Cliff's delta, raw and adjusted p-values for all ten genes.
- `figures/`: Violin plot showing expression distributions for all ten genes across both tumor groups, annotated with adjusted p-values.

## References

1. Cancer Genome Atlas Research Network. Comprehensive, integrative genomic analysis of diffuse lower-grade gliomas. *New England Journal of Medicine*. 2015;372:2481-2498.
2. Goldman MJ, Craft B, Hastie M, et al. Visualizing and interpreting cancer genomics data via the Xena platform. *Nature Biotechnology*. 2020;38:675-678.
3. UCSC Xena. TCGA lower-grade glioma and glioblastoma (GBMLGG) cohort and data resources. Dataset: `TCGA.GBMLGG.sampleMap/HiSeqV2`.

## Author

Swasti Maurya
Incoming Biological Sciences BS student, University at Buffalo (Spring 2027)
www.linkedin.com/in/swasti-maurya
