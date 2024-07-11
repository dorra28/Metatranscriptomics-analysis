Metatranscriptomics and Microbiome Analysis
Introduction
This repository contains scripts and documentation for the analysis of metatranscriptomic data and microbiome composition.

Methods
1. Metatranscriptomics Analysis
Data Exploitation
A total of 34 clinical nasopharyngeal swab (NPS) samples were collected from the Institut Pasteur de Tunis as part of an international project on SARS-CoV-2.
Samples included 23 positive and 11 negative cases, collected between November 2021 and January 2022.
Paired-end sequencing was performed using an Illumina Novaseq sequencer following standard Illumina protocols.
Data Analysis Environment and Tools
Computational analyses were conducted on the TESLA server at the Institut Pasteur de Tunis, equipped with:
Processor: Intel Xeon E5-2699v3, 2.3 GHz
Cores: 72
RAM: 503 GB
Storage: 22 TB
Operating System: Debian
Programming languages utilized: Python, R, Bash.
Pipeline for Metatranscriptomic Analysis
Developed a custom pipeline to analyze metatranscriptomic data, focusing on interactions between respiratory RNA viruses, upper respiratory tract microorganisms, and host immune responses.
Quality assessment of sequencing data using FASTQC, MultiQC, and adapter trimming with Cutadapt.
Analysis for SARS-CoV-2
Alignment to the SARS-CoV-2 Reference Genome (NC_045512.2) using BWA-MEM:

bash

bwa mem -t 8 reference_genome.fasta reads.fastq > alignment.sam
Variant Calling using Snippy:

bash

snippy --cpus 8 --reference reference.fasta --R1 reads_R1.fastq --R2 reads_R2.fastq
Variant Annotation with SnpEff:

bash

java -jar snpEff.jar -v -stats variants.html genome_version variants.vcf > annotated.vcf
Genome Sequence Reconstruction with SPAdes:

bash

spades.py -1 reads_R1.fastq -2 reads_R2.fastq -o output_directory
Host Analyses
Alignment to the Human Reference Genome (GRCh38.dna.alt.fa) using BWA:

bash

bwa mem -t 8 human_genome.fasta sample_reads.fastq > alignment.sam
Quantification of Human Genes with FeatureCount:

bash

featureCounts -T 8 -a annotation.gtf -o counts.txt input.bam
2. Microbiome Analysis
Bacterial Species Identification
Using Kraken2 (v2.1.2) to Identify and Quantify Bacterial Species:

bash

kraken2 --paired --quality-threshold 20 --min-hits-groups 2 --db standard_db sample_R1.fastq sample_R2.fastq > kraken2_output.txt
Visualization with PAVIAN Metagenomics Data Explorer:

Download PAVIAN from PAVIAN GitHub Repository.
Launch PAVIAN and import kraken2_output.txt for visualization.
Data Visualization and Alpha Diversity Analysis in R
