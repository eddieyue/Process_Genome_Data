Genome Data
============

I use the Genome data from Data Access Layer(DAL) https://github.com/cioc/DAL, which is a library that makes it easy to use the datasets. 

For this project, I work with the over 10 gigabytes Genome dataset and reconstruct the Cladogram by comparing with the similarity of those genomes.

The following bit of simple code to show how to extract and display them.

```python
from DAL import create
#create a handle to the Genome dataset
genomes = create("genomes")
#loading the genome data
genomes.subsets()->list(str)
#returns a list of all genomes in the project. 
genomes.k_mers(genome:str,length:int)->list(str)
#returns a generator of all k-­length strings of DNA from the given genome.
```

Compute the DNA distance matrix
===============================

I break up the genome finto strands files, then sort them and commbine all sorted strand files together by heapq.merge. By scanning the combined strand file, I construct a similarity matrix by check which genomes have DNA in common.

Reconstruct Cladogram
=====================

By using the similarity matrix, I generate a list of all pairs of genomes sorted by their similarity. Do agglomerative hierarchical clustering with the single linkage and print out all grouping events in chronological order. 