---
layout: default
---

### Fourth Exercise

You will have two input files: train.fa and test.fa.

Both will contain multiple fasta records with names. 

Each record is a gene sequence starting at the first codon (ATG).

For each sequence, compute a vector which contains the frequency with which each codon appears in each gene.

For each item in the test set find the closest item in the training set, as defined by euclidean distance between the corresponding frequency vectors.

Print the matches (test set name, train set name, distance).

Find the first two principal components of the training data and project all frequency vectors onto the space they define. Produce a 2d scatterplot with the projections of the training set data in blue and the test set data in red.

Optional: draw a gray connecting line between the test set items and their closest training set item.