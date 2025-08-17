# DNAseq Variant Calling Pipeline (hg38)

A comprehensive workflow for variant calling from raw FASTQ files using GATK (or SAMtools) methodologies, aligned to the hg38 reference genome.

## Workflow Overview

<img width="500" height="900" alt="image" src="https://github.com/user-attachments/assets/581e2882-ee53-463d-9cb6-63cbe9be277d"/>

1. Reference genome preparation
2. Read alignment with BWA-MEM
3. Quality control with FastQC
4. Duplicate removal with Picard
5. Variant calling with:
   - GATK HaplotypeCaller
   - SAMtools
6. Variant filtering and annotation

## Prerequisites

### Software Requirements
- [bwa](http://bio-bwa.sourceforge.net/) (v0.7.17+)
- [bcftools](http://www.htslib.org/) (v1.15+)
- [FastQC](https://www.bioinformatics.babraham.ac.uk/projects/fastqc/) (v0.11.9+)
- [Picard](https://broadinstitute.github.io/picard/) (v2.27+)
- [GATK](https://gatk.broadinstitute.org/) (v4.3.0.0+)
- [samtools](http://www.htslib.org/) (v1.15+)
- [SnpEff/SnpSift](https://pcingola.github.io/SnpEff/) (v5.1+)

### Reference Data
- hg38 reference genome (download from [UCSC](https://hgdownload.soe.ucsc.edu/goldenPath/hg38/bigZips/))
- Corresponding BWA index files
- Known variants databases (for BQSR if needed)

## Output Files

- sorted_SRR14634773.bam → Sorted BAM file
- rmdup_SRR14634773.bam → Deduplicated BAM file
- picard_output.bam → Final BAM with read groups
- GATK_variation_calling.vcf → Variants called with GATK
- bcftools_variation_output.vcf → Variants called with SAMtools/bcftools
- snpSift_output.vcf / bcftools_snpSift_output.vcf → Filtered variants

## Notes

- Use GATK HaplotypeCaller for germline variant calling.
- Use GATK Mutect2 (not shown here) for somatic variant calling.
- Adjust filtering thresholds (QUAL, DP, MQ) based on your dataset. 

## Installation

```bash
# Clone this repository
git clone https://github.com/yourusername/DNAseq-for-variant-analysis.git
cd DNAseq-for-variant-analysis

# Download reference genome (example)
wget https://hgdownload.soe.ucsc.edu/goldenPath/hg38/bigZips/hg38.fa.gz
gunzip hg38.fa.gz
bwa index hg38.fa
