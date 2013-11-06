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

[genome.fz.gz](http://bx.mathcs.emory.edu/outgoing/genome.fa.gz)

### Tim's solution

```python
#!/usr/bin/python
def readFastaSeq(seqfile):
    fh = open(seqfile)
    name = fh.readline()[1:-1]  #can return if you need to
    sequence = ""
    for line in fh:
        sequence += line.replace('\n','')
    return(sequence)

def transSeq(subseq):
    gencode = {
    'ATA':'I', 'ATC':'I', 'ATT':'I', 'ATG':'M',
    'ACA':'T', 'ACC':'T', 'ACG':'T', 'ACT':'T',
    'AAC':'N', 'AAT':'N', 'AAA':'K', 'AAG':'K',
    'AGC':'S', 'AGT':'S', 'AGA':'R', 'AGG':'R',
    'CTA':'L', 'CTC':'L', 'CTG':'L', 'CTT':'L',
    'CCA':'P', 'CCC':'P', 'CCG':'P', 'CCT':'P',
    'CAC':'H', 'CAT':'H', 'CAA':'Q', 'CAG':'Q',
    'CGA':'R', 'CGC':'R', 'CGG':'R', 'CGT':'R',
    'GTA':'V', 'GTC':'V', 'GTG':'V', 'GTT':'V',
    'GCA':'A', 'GCC':'A', 'GCG':'A', 'GCT':'A',
    'GAC':'D', 'GAT':'D', 'GAA':'E', 'GAG':'E',
    'GGA':'G', 'GGC':'G', 'GGG':'G', 'GGT':'G',
    'TCA':'S', 'TCC':'S', 'TCG':'S', 'TCT':'S',
    'TTC':'F', 'TTT':'F', 'TTA':'L', 'TTG':'L',
    'TAC':'Y', 'TAT':'Y', 'TAA':'_', 'TAG':'_',
    'TGC':'C', 'TGT':'C', 'TGA':'_', 'TGG':'W'}
    pep = ""
    flag = 0
    for i in range(0,(len(subseq)/3)-1):
        codon = subseq[(i*3):(i*3+3)]
        if codon == 'ATG':
            flag = 1
            pep += gencode.get(codon)
        elif codon in ['TAA','TGA','TAG']:
            flag = 0
            pep += gencode.get(codon)
        elif flag == 1:
            pep += gencode.get(codon)
        else:
            pass
    return(pep)

def revTrans(seqfile):
    import string
    return(seqfile.translate(string.maketrans("ATCG", "TAGC"))[::-1])

def outputProt(pepstr,header,cutoff):
    peplist = pepstr.split('_')
    j = 1
    for pep in peplist:
        if len(pep) > cutoff:
            print(">"+header+str(j)+"\n"+pep)
            j += 1

def main(infile):
    import pdb
    seq = readFastaSeq(infile)
    rev = revTrans(seq)
    outputProt(transSeq(seq[0:]),"frame1-",50)
    outputProt(transSeq(seq[1:]),"frame2-",50)
    outputProt(transSeq(seq[2:]),"frame3-",50)
    outputProt(transSeq(rev[0:]),"frame4-",50)
    outputProt(transSeq(rev[1:]),"frame5-",50)
    outputProt(transSeq(rev[2:]),"frame6-",50)

if __name__ == "__main__":
    import sys
    main("./genome.fa")
```