# RNA-seq_Analysis
End-to-end RNA-seq analysis pipeline (QC, trimming, alignment, counting, differential expression)(Paired-end reads)

# RNA-seq Analysis Pipeline

This repository contains a complete RNA-seq data analysis workflow used in my MSc research.

## Pipeline Overview
1. **Quality Control:** `FastQC`, `MultiQC`
2. **Trimming:** `Trimmomatic`
3. **Quality Control:** `FastQC`, `MultiQC`
4. **Alignment:** `STAR`
5. **Counting:** `featureCounts`
6. **Differential Expression:** `Limma-voom`
7. **Visualization:** MDS-Plot, Heatmap

## Example Usage
```bash
# Quality Control
fastqc *.fq.gz -o FastQC_out
multiqc FastQC_out -o MultiQC_out

##Trim if need be based on results after initial trimming
trimmomatic PE -phred33 input_R1.fq.gz input_R2.fq.gz input_R1_P.fq.gz input_R1_U.fq.gz input_R2_P.fq.gz input_R2_U.fq.gz HEADCROP:10 SLIDINGWINDOW:3:20 MINLEN:20

#Quality control
fastqc *_R1_P.fq.gz *_R2_P.fq.gz -o FastQC_trimmed_out
multiqc FastQC_trimmed_out -o MultiQC_trimmed_out

# Alignment
STAR --runThreadN 8 --genomeDir genome_index --readFilesIn sample_R1.fq.gz sample_R2.fq.gz --readFilesCommand zcat --outFileNamePrefix sample_

# Counting
featureCounts -a annotation.gtf -o counts.txt *.bam
#DE_Analysis in R
**Differential analysis**
**Visualization**
