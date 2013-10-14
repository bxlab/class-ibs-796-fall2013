---
layout: default
---

### First Exercise

From the latest 1000 genomes release, get the variant calls for chr22 in VCF format (ftp://ftp-trace.ncbi.nih.gov/1000genomes/ftp/release/20110521/). 

Write a Python script which reads from the VCF all SNPs with minor allele frequency greater than 5% (note that VCF files also contain other types of variants), and computes the linkage disequilibrium between each pair. 

Identify contiguous runs of linked variants (LD > 0). Produce a plot showing both the raw LD score for each adjacent pair and the linked blocks. 
