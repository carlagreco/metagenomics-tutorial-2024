# Metagenomics tutorial
Dr Carla Greco
September 2024

## Introduction

The aim of this quick tutorial is to classify metagenomic using Kraken2

##Getting started
### 1. Setup your working directory
- So we don't overwrite each other's work please make a directory to work in
- you can call it anything, but your name would be useful
```
mkdir carla
cd carla
```

### 3. Take a look at the data
- The data used in this tutorial is located in `/data`
- You will see two files (using command `ls`) -  this is pair-ended illumina data
- Take a look at the files with:
```
zcat /data/SampleA_R1.fastq.gz | head
zcat /data/SampleA_R2.fastq.gz | head
```

### 4. Clean up the data
- It is important to remove barcodes and low quality reads in your dataset
- We will do this with automated fastq proccessor [fastp](https://github.com/OpenGene/fastp)
- Look at the fastp documentation with `fastp -h`
- Run the command to QC and clean up data

```
fastp -i /data/SampleA_R1.fastq.gz -I /data/SampleA_R2.fastq.gz -o SampleA_trim_R1.fastq.gz -O SampleA_trim_R2.fastq.gz -j SampleA_fastp.json -h SampleA_fastp.html
```

- Take a took at the html report:
    - Were the adapters that were expected removed?
    - How many reads made it through the trimming?

### 5. Take a look at the Kraken2 documentation
- [Kraken2](https://github.com/DerrickWood/kraken2) is a fast kmer-based metagenomic classification tool
- Use this command to read the help page
`kraken2 -h`

- The kraken2 database we will be using is located in `/db` you can take a look at the files with the `ls` command


### 6. Run kraken2
- The command to run kraken2 is:

```
kraken2 --threads 1 --db /db/k2 --output SampleA_output.txt --report SampleA_kraken.report --paired SampleA_trim_R1.fastq.gz SampleA_trim_R2.fastq.gz
```
- This command runs:

- Take a look at the report (type q to exit viewer):
```
less SampleA_kraken.report
```
The report file contains a hierarchical output file in the followinf format:

1. Percentage of fragments covered by the clade rooted at this taxon
2. Number of fragments covered by the clade rooted at this taxon
3. Number of fragments assigned directly to this taxon
4. A rank code, indicating (U)nclassified, (R)oot, (D)omain, (K)ingdom, (P)hylum, (C)lass, (O)rder, (F)amily, (G)enus, or (S)pecies. Taxa that are not at any of these 10 ranks have a rank code that is formed by using the rank code of the closest ancestor rank with a number indicating the distance from that rank. E.g., "G2" is a rank code indicating a taxon is between genus and species and the grandparent taxon is at the genus rank.
5. NCBI taxonomic ID number
6. Indented scientific name


### 7. View results in a Krona plot

```
ktImportTaxonomy -t 5 -m 3 -o SampleA_krona.html SampleA_kraken.report 
```

- Where do you think this sample came from?

### 8. Done? try another sample

```
wget ftp://ftp.sra.ebi.ac.uk/vol1/fastq/DRR053/DRR053207/DRR053207_1.fastq.gz
wget ftp://ftp.sra.ebi.ac.uk/vol1/fastq/DRR053/DRR053207/DRR053207_2.fastq.gz
```
