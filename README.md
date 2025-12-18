# RNA-Seq Analysis — End-to-End Workflow  
(QC → Alignment → DGE → Enrichment → ML)

This repository documents a complete RNA-seq workflow starting from raw FASTQ files and moving through:

- Quality control and preprocessing (Linux tools)  
- Genome alignment (STAR)  
- Gene quantification (featureCounts)  
- Differential gene expression (DESeq2)  
- Functional enrichment (clusterProfiler)  
- Exploratory machine learning classification (scikit-learn)  

The purpose of this project is learning and practicing a full transcriptomics workflow, not building a clinical-grade model.

---

## Project Overview

This project revisits an RNA-seq assignment and demonstrates:

- End-to-end processing of RNA-seq data  
- How raw reads become quantifiable gene counts  
- How DESeq2 identifies biologically meaningful genes  
- How enrichment analysis reveals pathways  
- How machine learning can be applied exploratorily to gene expression  

This repository reflects a complete transcriptomics workflow in a single place.

---

## Files in This Repository

The repository contains the following standalone scripts (no subfolders):

    README.md
    linux_pipeline.sh
    dge_analysis.R
    mutation_classifier.py

---

## Workflow Summary

### 1. Raw Data Processing (Linux Script)

**File:** `linux_pipeline.sh`

Includes commands for:

- Downloading SRA FASTQ files  
- Running FastQC (quality control)  
- Trimming reads using fastp  
- Aligning reads to GRCh38 using STAR  
- Generating gene-level read counts using featureCounts  

Outputs of this step:

- Trimmed FASTQ files  
- Alignment BAM file  
- `gene_counts.txt` (raw count matrix)  

---

### 2. Differential Gene Expression (DESeq2)

**File:** `dge_analysis.R`

Key steps:

- Import count matrix and metadata  
- Verify sample IDs  
- Normalize counts using DESeq2  
- Perform contrast: siRNA against p53 vs negative control siRNA  
- Filter significant DEGs (`padj < 0.05` and `|log2FC| > 1`)  

Generates:

- Volcano plot  
- Heatmap of top 50 DEGs  

Outputs are saved as CSV files and plots when the script is run.

---

### 3. Functional Enrichment (clusterProfiler)

Included within `dge_analysis.R`.

Steps:

- Convert ENSEMBL IDs to ENTREZ IDs  
- Run GO Biological Process enrichment  
- Produce dotplot visualization  

This connects statistically significant DEGs to biological interpretation.

---

### 4. Exploratory Machine Learning (Python)

**File:** `mutation_classifier.py`

Purpose: practice ML workflows on gene-expression–like data.  
(Not intended for biological prediction due to small sample size.)

Pipeline includes:

- Variance filtering  
- Selection of top 5,000 most variable genes  
- `SelectKBest` (ANOVA F-test)  
- Random Forest classifier  
- PCA visualization  
- ROC-AUC evaluation  
- Extraction of top contributing genes  

Outputs:

- PCA scatter plot  
- ROC curve  
- Feature importance rankings  

---

## Purpose of This Project

This project is for learning and skill-building, demonstrating:

- Full understanding of RNA-seq preprocessing  
- Ability to use DESeq2 for differential expression analysis  
- Capability to perform GO enrichment analysis  
- Exploratory use of machine learning on gene sets  
- Integration of Linux, R, and Python tools in one workflow  

It is not intended as a clinical diagnostic tool.

---

## Tools & Technologies Used

### Linux / NGS
- SRA Toolkit  
- FastQC  
- fastp  
- STAR  
- Subread (featureCounts)  

### R
- DESeq2  
- pheatmap  
- ggplot2  
- org.Hs.eg.db  
- clusterProfiler  
- enrichplot  

### Python
- pandas  
- numpy  
- scikit-learn  
- matplotlib  

---

## Future Improvements

- Add Snakemake workflow for automation  
- Replace STAR with lightweight quantifiers (Salmon / Kallisto)  
- Add batch correction (if metadata available)  
- Package ML workflow into a Jupyter notebook  

---

## Learning Takeaways

- Practiced complete RNA-seq analysis from raw reads to insights  
- Understood how DESeq2 identifies differentially expressed genes  
- Explored pathway enrichment using biological ontologies  
- Experimented with machine-learning techniques for expression data  

