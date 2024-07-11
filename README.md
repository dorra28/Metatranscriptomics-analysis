# Metatranscriptomics-analysis
This repository contains code and data for a metatranscriptomics study on COVID-19. We analyze SARS-CoV-2 and host transcriptomes to understand their interactions in patients. The project includes viral and host transcriptome analyses, and interaction networks using high-throughput sequencing and bioinformatics tools
# Metatranscriptomics Analysis Project

## Overview

This project aims to analyze metatranscriptomic data from COVID-19 patients to understand the interactions between SARS-CoV-2 and the host immune response.

## Data

- **Samples:** 34 clinical samples collected from nasopharyngeal swabs.
- **Sequencing:** Paired-end sequencing on Illumina sequencer.

## Computational Environment

- **Server:** TESLA server at BIMS, IPT.
  - **Specifications:** Intel Xeon E5-2699v3, 72 cores, 503 GB RAM, 22 TB storage, Debian OS.
- **Languages:** Python, R, Bash.

## Analysis Pipeline

### Preprocessing

- Quality assessment with `FastQC`.
- Multi-sample QC with `MultiQC`.
- Adapter trimming with `Cutadapt`.

### Alignment and Variant Calling

- Alignment to SARS-CoV-2 genome (`BWA-MEM`).
- Variant calling using tools like `Snippy`, `GATK`, `Bcftools`, `Lofreq`.

### Annotation and Interpretation

- Functional annotation with `SnpEff`.
- Phylogenetic analysis using `Nextclade`.
