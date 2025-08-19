# show_3RACE_primers_on_tracks

This document describes the usage of a simple pipeline to align 3'RACE primer sequences to the human genome (hg38), convert alignment files, and generate BED format coordinates for visualization on genomic tracks or further analysis.

---

## Prerequisites

- **Bowtie2** installed and accessible in your PATH  
- **Samtools** installed and accessible  
- **Bedtools** installed and accessible  
- Indexed hg38 reference genome for Bowtie2 located at:  
  `/path/to/bowtie2_index/hg38`  
- Primer sequences in FASTA format prepared in `/path/to/fasta_files/`  
- Output directories:  
  - SAM and BAM files in `/path/to/bams/`  
  - BED files in `/path/to/bed_files/`  

---

## Pipeline Description

This pipeline takes a primer FASTA file (containing forward and reverse primers), aligns the primers to the hg38 reference genome using Bowtie2, converts the alignments from SAM to BAM format using samtools, and converts the BAM alignments to BED format using bedtools.

---

## Commands

file_name="example"

Align primers to hg38 with Bowtie2, output SAM file
bowtie2 -x /path/to/bowtie2_index/hg38
-f /path/to/fasta_files/${file_name}.fasta
-S ./bams/${file_name}.sam

Convert SAM to BAM with header
samtools view -b -h ./bams/${file_name}.sam > ./bams/${file_name}.bam

Convert BAM to BED format
bedtools bamtobed -i ./bams/${file_name}.bam > ./bed_files/${file_name}.bed

---

## Notes

- Adjust the `file_name` variable to the file name of interest.  
- Ensure all required directories (`/path/to/fasta_files/`, `/path/to/bams/`, `/path/to/bed_files/`) exist before running.  
- The BAM and BED files facilitate downstream analysis and visualization (e.g., in genome browsers).  

---

## References

- [Bowtie2](http://bowtie-bio.sourceforge.net/bowtie2/index.shtml)  
- [Samtools](http://www.htslib.org/)  
- [Bedtools](https://bedtools.readthedocs.io/en/latest/)  

---
