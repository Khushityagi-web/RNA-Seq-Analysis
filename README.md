# RNA-Seq Analysis — End-to-End Workflow (QC → Alignment → DGE → Enrichment → ML)

This repository documents a complete RNA-seq workflow starting from raw FASTQ files and moving through:

Quality control & preprocessing (Linux tools)

Genome alignment (STAR)

Gene quantification (featureCounts)

Differential gene expression (DESeq2)

Functional enrichment (clusterProfiler)

Exploratory ML classification (scikit-learn)

The purpose of this project is learning and practicing a full transcriptomics workflow, not building a clinical-grade model.

## 📌 Project Overview

This project revisits is a RNA-seq assignment:

end-to-end processing of RNA-seq data

how raw reads become quantifiable gene counts

how DESeq2 identifies biologically meaningful genes

how enrichment analysis reveals pathways

how machine learning can be applied exploratorily to gene expression

This repo reflects a complete transcriptomics workflow in a single place.

## 📁 Files in This Repository

The repo contains these actual files/scripts:

README.md
linux_pipeline.sh        # preprocessing → QC → trimming → alignment → counts
dge_analysis.R           # DESeq2 workflow + volcano + heatmap + GO enrichment
mutation_classifier.py   # ML workflow on gene expression matrix


There are no folders, only standalone scripts.

## 🧬 Workflow Summary
### 1. Raw Data Processing (Linux Script)

File: linux_pipeline.sh

Includes commands for:

downloading SRA FASTQ files

running FastQC (quality check)

trimming reads using fastp

aligning reads to GRCh38 using STAR

generating gene-level read counts using featureCounts

Outputs of this step:

trimmed FASTQs

alignment BAM file

gene_counts.txt (raw count matrix)

### 2. Differential Gene Expression (DESeq2)

File: dge_analysis.R

Key steps:

imports count matrix + metadata

verifies sample IDs

normalizes counts with DESeq2

performs contrast:
siRNA against p53 vs negative control siRNA

filters significant DEGs (padj < 0.05 & |log2FC| > 1)

generates:

volcano plot

heatmap of top 50 DEGs

Outputs are saved as CSVs and plots when the script is ran.

### 3. Functional Enrichment (clusterProfiler)

Included inside dge_analysis.R.

Steps:

converts ENSEMBL IDs to ENTREZ

runs GO Biological Process enrichment

produces dotplot visualization

This connects statistical DEGs to biological interpretation.

### 4. Exploratory Machine Learning (Python)

File: mutation_classifier.py

Purpose: practice ML workflows on gene-expression–like data
(Not intended for biological prediction due to small sample size.)

Pipeline includes:

variance filtering

selecting top 5,000 variable genes

SelectKBest (ANOVA F-test)

RandomForest classifier

PCA visualization

ROC-AUC evaluation

extraction of top contributing genes

Outputs:

PCA scatter plot

ROC curve

feature importance rankings

## 🎯 Purpose of This Project

This project is for learning and skill-building, showing:

full understanding of RNA-seq preprocessing

ability to use DESeq2 for differential expression

capability to perform GO enrichment analysis

exploratory use of machine learning on gene sets

ability to integrate Linux, R, and Python tools in one workflow

It is not intended as a clinical diagnostic tool.

## 🔧 Tools & Technologies Used
Linux / NGS

SRA Toolkit

FastQC

fastp

STAR

Subread (featureCounts)

R

DESeq2

pheatmap

ggplot2

org.Hs.eg.db

clusterProfiler

enrichplot

Python

pandas, numpy

scikit-learn

matplotlib

## 📈 Future Improvements

Add Snakemake workflow for automation

Replace STAR with lightweight quantifiers (Salmon/Kallisto)

Add batch correction (if metadata available)

Package ML workflow into a Jupyter notebook

## 📚 Learning Takeaways

Practiced complete RNA-seq analysis from raw reads to insights

Understood how DESeq2 identifies DE genes

Explored pathway enrichment using biological ontologies

Experimented with machine-learning techniques for expression data
