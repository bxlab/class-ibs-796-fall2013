---
layout: default
---

### Second Exercise

Your input is a file containing genomic DNA in FASTA format

* The input contains an unknown number of genes
* There are no introns
* Each gene contains at least 10 codons
* The standard genetic code is used

You should implement a program which identifies all genes in the genome and prints:

* Amino acid sequence of each gene

### Timing in Python

Accurate timing requires running a program many times and taking the average of the runtime (otherwise it might be confounded by other activities taking place on the system at the same time). The `timeit` module in Python makes this easy. For more details, see [`timeit` on PyMOTW](http://pymotw.com/2/timeit/). 

### Data file to test on

[genome.fz.gz](ihttp://bx.mathcs.emory.edu/outgoing/genome.fa.gz)
