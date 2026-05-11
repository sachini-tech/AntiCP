# AntiCP 2.0: Anticancer Peptide Prediction Tool

Welcome to the official repository for AntiCP 2.0, an updated and improved computational method for predicting and designing anticancer peptides (ACPs) from amino acid sequences. This resource is designed to support researchers in peptide therapeutics, cancer biology, and computational drug discovery.

**Web Server:** https://webs.iiitd.edu.in/raghava/anticp2/
**Standalone (GitHub):** https://github.com/raghavagps/anticp2/
**Docker Container:** https://webs.iiitd.edu.in/gpsrdocker/

ZENODO : https://doi.org/10.5281/zenodo.20083367

---

## Citation

Agrawal, P., Bhagat, D., Mahalwal, M., Sharma, N., & Raghava, G. P. S. (2021).
AntiCP 2.0: an updated model for predicting anticancer peptides.
*Briefings in Bioinformatics*, 22(3), bbaa153.
https://doi.org/10.1093/bib/bbaa153

---

## About the Tool

AntiCP 2.0 is an updated version of the original AntiCP method, developed to predict and design anticancer peptides using multiple machine learning classifiers trained on the largest available dataset. It consolidates sequence-level features — composition, binary profiles, terminus patterns, and motifs — into a unified prediction framework, enabling systematic identification and design of ACPs from raw amino acid sequences.

The tool integrates data from:

* CancerPPD database (anticancer peptides)
* ACP-DL, ACPP, ACPred-FL, AntiCP and iACP datasets
* SwissProt (for random peptide generation in alternate dataset)

---

## Key Features

**Two Curated Datasets**

* Main dataset: 861 ACPs vs. 861 AMPs (non-ACPs)
* Alternate dataset: 970 ACPs vs. 970 random peptides
* 80/20 split for training and validation

**Rich Feature Extraction**

* Amino Acid Composition (AAC) — 20-dimensional vector
* Dipeptide Composition (DPC) — 400-dimensional vector
* Terminus Composition — N5, N10, N15, C5, C10, C15, and combined
* Binary Profile — captures residue order (not just composition)
* Hybrid Features — composition + binary profile + motif

**Multiple Machine Learning Classifiers**

* Support Vector Machine (SVM)
* Random Forest (RF)
* Extra Trees (ETree)
* K-Nearest Neighbors (KNN)
* Artificial Neural Network / MLP
* Ridge Classifier

**Motif Analysis**

* Exclusive ACP motifs identified: `LAKLA`, `AKLAK`, `FAKL`, `LAKL`
* Exclusive non-ACP motifs identified: `GLW`, `CKIK`, `DLV`, `AGKG`
* Identified using MERCI (Motif-EmeRging and with Classes-Identification) software

**Web Server Modules**

* Predict — anticancer potency of submitted peptides
* Design — generate and score single-mutation variants
* Protein Scan — scan overlapping windows in a protein sequence
* Motif Scan — check for exclusive ACP motifs
* Download — download datasets in FASTA format

---

## Overview

AntiCP 2.0 provides machine learning-based prediction along with:

* Binary classification of ACPs vs. non-ACPs (main and alternate models)
* Residue composition and positional preference analysis
* Exclusive motif identification in ACPs
* Novel ACP design via single-mutation scanning
* Protein-level scanning for anticancer regions
* Standalone and Docker-based deployment options

---

### Residue Composition Insights

Analysis of ACPs revealed the following key observations:

* **Enriched residues in ACPs:** A, F, K, L, W (positively charged and aromatic)
* **N-terminus preference:** F at position 1, A at position 2, K at position 3; L preferred at other positions
* **C-terminus preference:** L and K are highly enriched
* **Non-ACP enriched residues:** C, G, R, S

---

### Best Model Performance — Main Dataset

| Feature | Classifier | MCC (Train) | AUROC (Train) | MCC (Val) | AUROC (Val) |
|---------|-----------|-------------|---------------|-----------|-------------|
| AAC | ETree (400) | 0.49 | 0.82 | 0.48 | 0.83 |
| DPC | ETree (400) | 0.51 | 0.83 | 0.51 | 0.83 |
| Binary N10C10 | SVM | 0.45 | 0.81 | 0.46 | 0.81 |
| AAC + Motif | SVM | 0.49 | 0.83 | 0.45 | 0.82 |
| DPC + Bin_N10C10 | SVM | 0.47 | 0.81 | 0.48 | 0.81 |

### Best Model Performance — Alternate Dataset

| Feature | Classifier | MCC (Train) | AUROC (Train) | MCC (Val) | AUROC (Val) |
|---------|-----------|-------------|---------------|-----------|-------------|
| AAC | ETree (400) | 0.80 | 0.97 | 0.84 | 0.97 |
| DPC | ETree (400) | 0.80 | 0.96 | 0.81 | 0.96 |
| Binary N15C15 | SVM | 0.75 | 0.95 | 0.76 | 0.95 |
| AAC + Bin_N15C15 | SVM | 0.84 | 0.98 | 0.86 | 0.97 |
| AAC + Motif | SVM | 0.84 | 0.98 | 0.81 | 0.97 |

---

### Benchmarking Against Existing Methods

AntiCP 2.0 outperformed all existing methods on both datasets:

| Method | Main Dataset MCC | Alternate Dataset MCC |
|--------|-----------------|----------------------|
| **AntiCP 2.0** | **0.51** | **0.84** |
| AntiCP | 0.07 | 0.80 |
| ACPred | 0.09 | 0.71 |
| ACPred-FL | -0.12 | -0.15 |
| ACPpred-Fuse | 0.38 | 0.60 |
| PEPred-Suite | 0.08 | 0.16 |
| iACP | 0.11 | 0.55 |

> On the independent dataset used in ACPred-Fuse, AntiCP 2.0 achieved MCC 0.47 vs. ACPred-Fuse MCC 0.32.

---

### Improvements Over Previous Version (AntiCP)

* Largest dataset used to date for ACP prediction
* Added dipeptide composition (DPC) as a feature
* Added binary profile models for capturing residue order
* Added hybrid models combining composition + binary profile + motif
* Two separate datasets (main and alternate) for comprehensive evaluation
* Standalone Python software and Docker container support
* Responsive web server compatible with mobile devices (iPhone, iPad, Android)

---

### Limitations

* Structural properties not considered (secondary structure, surface accessibility, disulfide bonds)
* Post-translational modifications (terminus modifications, glycosylation, phosphorylation) not incorporated
* Peptide length restricted to 4–50 residues for web server prediction
* Terminal binary models require minimum peptide length matching the profile (e.g., N15C15 needs ≥15 residues)
* High similarity between ACPs and AMPs makes main dataset discrimination harder than alternate dataset

---

## Applications

* Anticancer peptide discovery and design
* Scanning proteins for potential anticancer regions
* Machine learning model benchmarking for ACP research
* Peptide-based cancer drug development
* Rational design of ACP mutants with enhanced potency

---

## Contact & Authors

**Prof. Gajendra P. S. Raghava**
raghava@iiitd.ac.in
Department of Computational Biology, Indraprastha Institute of Information Technology (IIIT Delhi)
Okhla Phase 3, New Delhi-110020, India
http://webs.iiitd.edu.in/raghava/

**Piyush Agrawal** — Research Associate-I, Dept. of Computational Biology, IIIT Delhi
**Neelam Sharma** — PhD Scholar, Dept. of Computational Biology, IIIT Delhi

Developed at **Indraprastha Institute of Information Technology (IIIT Delhi), India**

---

## License

This tool is distributed under the terms of the
**Oxford University Press Standard License**
© The Author(s) 2020. Published by Oxford University Press. All rights reserved.

---

## Acknowledgements

Supported by:

* J.C. Bose National Fellowship, Department of Science and Technology (DST), Government of India
* DST-INSPIRE Fellowship

We thank Mr Sumeet Patiyal for assistance with the web server, and all researchers whose published work on anticancer peptides contributed to this dataset.
