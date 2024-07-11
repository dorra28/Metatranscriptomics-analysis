# Metatranscriptomics Study of SARS-CoV-2 Interactions

This repository contains code and documentation for a metatranscriptomics study focusing on the interactions between SARS-CoV-2 and its host in COVID-19 patients.

## Project Overview

This project explores the dynamics of SARS-CoV-2 infection through metatranscriptomic analysis. The study aims to deepen our understanding of virus-host interactions using novel computational approaches.

## Methods

### Exploitation of High-Throughput Sequencing Data

A total of 34 clinical nasopharyngeal swab (NPS) samples were collected from the Virology Service of Institut Pasteur de Tunis as part of an international project on SARS-CoV-2 funded by AGYA. Ethical approval was obtained from the Ethics Committee of Institut Pasteur de Tunis. The samples included 23 positive cases and 11 negative cases, collected between November 2021 and January 2022.

Sequencing was performed in paired-end mode on an Illumina Novaseq sequencer, following Illumina's detailed protocol.

### Metatranscriptomic Data Analysis

#### Environment and Prerequisites

The analysis was conducted on the TESLA server at the BIMS laboratory, Institut Pasteur de Tunis. TESLA is a specialized computing system for processing and analyzing complex biological data. It features:
- Processor: INTEL Xeon E5-2699v3 (2.3 GHz, 72 cores)
- RAM: 503 GB
- Storage: 22 TB
- Operating System: Debian

Prerequisites included proficiency in Python, R, and Bash programming languages for developing custom analysis pipelines and processing raw data files.

#### Pipeline for Data Analysis

In this study, a custom pipeline for metatranscriptomic data analysis was developed to investigate interactions between respiratory RNA viruses, other upper respiratory tract microorganisms, and host immune response.

#### Preprocessing

Quality assessment of sequencing data was performed using the following tools:
- **FASTQC**: 
  ```bash
  fastqc -o /output_directory input_file.fastq

-**MULTIQC**- 

```bash
multiqc /path_to_fastqc_outputs -o /output_directory

Adapter Trimming with Cutadapt 

```bash
cutadapt -a ADAPTER_SEQUENCE -o output.fastq input.fastq


### Variant Calling

Multiple tools were evaluated for variant calling, including Snippy, GATK, Bcftools, and Lofreq, based on read coverage and depth against the reference sequence.

### Functional Annotation

Plain textANTLR4BashCC#CSSCoffeeScriptCMakeDartDjangoDockerEJSErlangGitGoGraphQLGroovyHTMLJavaJavaScriptJSONJSXKotlinLaTeXLessLuaMakefileMarkdownMATLABMarkupObjective-CPerlPHPPowerShell.propertiesProtocol BuffersPythonRRubySass (Sass)Sass (Scss)SchemeSQLShellSwiftSVGTSXTypeScriptWebAssemblyYAMLXML`   bashCopier le codejava -jar snpEff.jar -v genome_version input.vcf > output.ann.vcf   `

### Genome Assembly

Plain textANTLR4BashCC#CSSCoffeeScriptCMakeDartDjangoDockerEJSErlangGitGoGraphQLGroovyHTMLJavaJavaScriptJSONJSXKotlinLaTeXLessLuaMakefileMarkdownMATLABMarkupObjective-CPerlPHPPowerShell.propertiesProtocol BuffersPythonRRubySass (Sass)Sass (Scss)SchemeSQLShellSwiftSVGTSXTypeScriptWebAssemblyYAMLXML`   spades.py -1 input_R1.fastq -2 input_R2.fastq -o output_directory   `

### Taxonomic Annotation

Plain textANTLR4BashCC#CSSCoffeeScriptCMakeDartDjangoDockerEJSErlangGitGoGraphQLGroovyHTMLJavaJavaScriptJSONJSXKotlinLaTeXLessLuaMakefileMarkdownMATLABMarkupObjective-CPerlPHPPowerShell.propertiesProtocol BuffersPythonRRubySass (Sass)Sass (Scss)SchemeSQLShellSwiftSVGTSXTypeScriptWebAssemblyYAMLXML`   mafft input_sequences.fasta > aligned_sequences.fasta  nextstrain build --input aligned_sequences.fasta --output output_directory   `

### Microbiome Analysis

#### Bacterial Species Identification

Plain textANTLR4BashCC#CSSCoffeeScriptCMakeDartDjangoDockerEJSErlangGitGoGraphQLGroovyHTMLJavaJavaScriptJSONJSXKotlinLaTeXLessLuaMakefileMarkdownMATLABMarkupObjective-CPerlPHPPowerShell.propertiesProtocol BuffersPythonRRubySass (Sass)Sass (Scss)SchemeSQLShellSwiftSVGTSXTypeScriptWebAssemblyYAMLXML`   kraken2 --paired --quality-threshold 20 --min-hits-groups 2 --db standard_db sample_R1.fastq sample_R2.fastq > kraken2_output.txt   `

### Visualization with PAVIAN

*   Download PAVIAN: [PAVIAN GitHub Repository](https://github.com/dnbaker/pavian)
    

#### Import Data

*   Launch PAVIAN and import kraken2\_output.txt for visualization.
    

### Data Visualization and Alpha Diversity Analysis in R

#### Quantification and Visualization

Plain textANTLR4BashCC#CSSCoffeeScriptCMakeDartDjangoDockerEJSErlangGitGoGraphQLGroovyHTMLJavaJavaScriptJSONJSXKotlinLaTeXLessLuaMakefileMarkdownMATLABMarkupObjective-CPerlPHPPowerShell.propertiesProtocol BuffersPythonRRubySass (Sass)Sass (Scss)SchemeSQLShellSwiftSVGTSXTypeScriptWebAssemblyYAMLXML`   library(tidyverse)  # Read microbiome data  data <- read.csv2("path_to_your_microbiome_data.csv", header = TRUE, na.strings = "")  # Reshape data to long format  data_long <- pivot_longer(data, cols = -OTU_ID, names_to = "Sample", values_to = "Abundance")  # Perform alpha diversity analysis  alpha_diversity <- data_long %>%    group_by(Sample) %>%    summarise(alpha_diversity = diversity(Abundance, index = "shannon"))  # Plotting  ggplot(alpha_diversity, aes(x = Sample, y = alpha_diversity)) +    geom_bar(stat = "identity", fill = "skyblue", color = "black") +    labs(title = "Alpha Diversity by Sample", x = "Sample", y = "Alpha Diversity") +    theme_minimal()   `



  
