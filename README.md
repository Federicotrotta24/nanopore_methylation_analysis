# Nanopore Methylation Analysis

## Overview

This repository contains an exploratory analysis of DNA methylation patterns using Oxford Nanopore sequencing data.

The objective is to characterize methylation at gene and promoter level and identify candidate regulatory regions, despite limited sequencing depth.

---

## Background

Oxford Nanopore sequencing enables direct detection of DNA methylation through signal-level information encoded in BAM files (MM/ML tags).

However, targeted sequencing panels often result in low coverage, which introduces important challenges for methylation analysis.

---

## Workflow

The analysis follows these main steps:

1. Extraction of methylation calls from Nanopore BAM files (MM/ML tags)
2. Conversion to tabular format
3. Intersection with genomic regions:
   - Gene bodies
   - Promoters
4. Aggregation of methylation at gene level
5. Filtering and prioritization of candidate genes

---

## Coverage limitations

Most CpG sites in this dataset have very low coverage (`valid_cov = 1`), leading to:

- Binary methylation values (0 or 1)
- Limited reliability of methylation estimates

Applying stricter coverage thresholds (e.g., ≥2 or ≥5) drastically reduced the number of available sites.

Therefore, the analysis was performed using:

- `valid_cov ≥ 1`

Results should be interpreted as exploratory due to:

- low sequencing depth
- lack of biological replicates

---

## Gene and promoter analysis

Methylation sites were mapped to:

- Gene bodies
- Promoter regions

Promoter-level analysis was prioritized due to its potential relevance in gene regulation.

Mitochondrial genes were excluded from downstream analysis to avoid bias, as they were highly represented.

---

## Candidate prioritization

Due to low coverage, the number of CpG sites per promoter (`n_sites`) was used as the main robustness criterion.

Two thresholds were defined:

- `n_sites ≥ 20`: initial candidate set (exploratory)
- `n_sites ≥ 50`: high-confidence candidate set

This approach balances data availability and robustness.

---

## Results

- Promoter-level aggregation allowed identification of candidate genes with moderate methylation signals
- Increasing `n_sites` threshold improved robustness of candidate selection
- No strong methylation signal was observed in well-known lung cancer genes

This may be explained by:

- limited coverage
- insufficient CpG representation in those regions
- or absence of strong promoter methylation in this dataset

---

## Preliminary conclusions

This analysis represents an exploratory framework for studying DNA methylation using Nanopore sequencing data.

Key insights:

- Coverage is a critical limiting factor in methylation analysis
- Aggregation at promoter level enables detection of candidate regions
- Filtering by CpG site count improves robustness

---

## Ongoing work

This project is currently in progress. Future steps include:

- Increasing sequencing depth or number of samples
- Integrating RNA-seq data
- Incorporating chromatin-related features
- Performing functional enrichment analysis

---

## Repository structure

nanopore_methylation_analysis/
│
├── notebooks/
│ └── 01_explore_methylation.ipynb
│
├── data/
│ ├── example_gene_intersection.tsv
│ └── example_promoter_intersection.tsv
│
├── results/
│ ├── gene_body_summary.tsv
│ ├── promoter_summary.tsv
│ ├── promoter_summary_nuclear.tsv
│ ├── candidate_promoters.tsv
│ └── strong_candidate_promoters.tsv
│
└── README.md


---

## Notes

- This repository contains a simplified version of the analysis
- Example data is included for demonstration purposes
- Full datasets are not provided due to size constraints

---

## Author

MD transitioning into bioinformatics, with a focus on epigenomics, transcriptomics, and computational biology.
