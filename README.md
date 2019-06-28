# scRNAseqVariantCalling

## Computation Pipeline

This pipeline aims to perform variant calling at the single cell level with the ultimate goal of one VCF file per cell as well as binary n_cell x n_snv matrix.

It consists of four subsequent main steps:

- align reads to a reference transcriptome using CellRanger

- split the BAM File into single cell specific BAM Files using bamCleave

- perform individual variant calling on each of the single cell specific BAM Files using the Picard Toolkit and GATK

- compute a binary n_cell x n_snv matrix using SSrGE


## Requirements

- CellRanger version 2.1.1

- BamCleave: https://warwick.ac.uk/fac/sci/systemsbiology/staff/dyer/software/bamcleave/

- featureCounts (included in the subread package): http://subread.sourceforge.net/

- Picard Toolkit version 2.20.2:  http://broadinstitute.github.io/picard/

- GATK version 3.8: https://software.broadinstitute.org/gatk/

- SSrGE: https://github.com/lanagarmire/SSrGE


## Step by Step


### 1. Alignment

- CellRanger version 2.1.1

- script: [alignment.sh](https://github.com/niklaslang/scRNAseqVariantCalling/blob/master/alignment.sh)

Alignment of the FASTQ Files using CellRanger version 2.1.1


### 2. Splitting BAM Files

- BamCleave: https://warwick.ac.uk/fac/sci/systemsbiology/staff/dyer/software/bamcleave/

- script: [bamCleave.sh](https://github.com/niklaslang/scRNAseqVariantCalling/blob/master/bamCleave.sh)

Splitting BAM files (CellRanger output) into single cell specific BAM files based on barcodes.
This means one BAM file per cell.

BamCleave identifies cells by the cell barcodes within the BAM file. Since there are far more cell barcodes than actual cells, BAM Cleave asks you to specify the number of cells N in advance. BamCleave then reads through the BAM file to find the N cell barcodes with the most reads and then creates one BAM files for each of those N barcodes.
Here, we simply use the number of cells estimated by CellRanger (therefore, see the web_summary.html in the CellRanger output folder).


### 3. Preprocessing BAM Files

- Picard Toolkit version 2.20.2:  http://broadinstitute.github.io/picard/

Preprocessing the the BAM Files is a far more complex than the previous steps. Hence, this step is subdivided in several substeps. Even though there's no problem in running all these steps from within one script, the steps vary greatly in terms of runtime and memory requirements. Therefore, we provide one short script for each step.

#### 3.1 Picard

#### 3.2 Picard

#### 3.3 Picard

#### 3.4 Picard

#### 3.5 Picard

#### 3.5 Picard

#### 3.6 Picard


### 4. Realignment and Recalibration

- GATK version 3.8: https://software.broadinstitute.org/gatk/

**CAVE:** make sure you work with GATK version 3.8 since there are substantial syntax differences between version 3.x and 4.x.


### 5. Variant Calling

- GATK version 3.8: https://software.broadinstitute.org/gatk/

**CAVE:** make sure you work with GATK version 3.8 since there are substantial syntax differences between version 3.x and 4.x.


### 6. Computing n_cell x n_snv matrix

- SSrGE: https://github.com/lanagarmire/SSrGE
