---
layout: default
---

### First Exercise

## Original Problem

From the latest 1000 genomes release, get the variant calls for chr22 in VCF format: (`ftp://ftp-trace.ncbi.nih.gov/1000genomes/ftp/release/20110521/`) 

*A small version of this file with just the 1st 1000 SNPs is available at* `http://bx.mathcs.emory.edu/outgoing/chr22_small.vcf.gz`

Write a Python script which reads from the VCF all SNPs with minor allele frequency greater than 5% (note that VCF files also contain other types of variants), and computes the linkage disequilibrium between each pair. 

Identify contiguous runs of linked variants (LD > 0). Produce a plot showing both the raw LD score for each adjacent pair and the linked blocks. 

# Example solution from class

This only prints the LD values, does not plot or determine blocks:

```python
#!/usr/bin/env python

"""
Compute linkage disequilibrium between adjacent SNPs with MAF > 0.5 from a 
1000 genomes formatted VCF file. 

Note: computes plink style genotype LD 
"""

from numpy import array, corrcoef
import sys

# Will be used to store name and genotype of last SNP
last = None
last_name = None

# Iterate over stdin line by line
for line in sys.stdin:
    # Ignore comment and header lines
    if line.startswith( "#" ): 
        continue
    # Remove trailing newlines and split on tabs
    fields = line.rstrip( "\r\n" ).split( "\t" )
    # SNP id (rs number) is in field 2
    name = fields[2]
    # Parse the INFO field (7) into a dictionary by splitting first on ';' 
    # and then on '='
    info = dict( pair.split( "=" ) for pair in fields[7].split(";") )
    # Pull the allele frequeny from the dictionary, if it is less than 5% go 
    # to the next SNP
    if float( info['AF'] ) < 0.05:
        continue
    # Parse the genotypes and convert from '0|1' format into integers from 
    # 0 to 2 indicating number of non-reference alleles
    next = array( [ sum( map( int, gt.split(":")[0].split("|") ) ) for gt in fields[9:] ] )
    # Continue if this is the first SNP we've seen
    if last is not None:
        # Print the LD as determined by computing the correlation coefficient
        # (corrcoef returns a 2x2 symmetric matrix in this case)
        print last_name, name, corrcoef( next, last )[0,1]
    # Current becomes previous for next iteration
    last = next
    last_name = name
```

## Additions to the problem

1. Compute the LD measure D' rather than using corrcoef, this will require counting different genotypes.


2. For the first 1000 SNPs, compute *all* pairwise LD values and produce an image plot in which each cell represents the LD of the pair of SNPs indexed by the X and Y axes. Use any of the LD approaches, try to be efficient. 


