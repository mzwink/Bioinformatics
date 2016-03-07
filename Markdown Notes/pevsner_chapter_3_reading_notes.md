## Pevsner Chapter 3 Reading Notes


### Protein Alignment

- More informative to compare protein sequences than DNA sequences because a change in DNA sequence does not necessarily change the amino acid that is specified

- Protein sequence comparisons can identify homologous sequences while corresponding DNA sequence comparisons cannot

- BLAST - allows related proteins derived from a DNA database to be searched for with a protein sequence

### Homology

- 2 sequences are homologous if they share a common evolutionary ancestry

- When 2 sequences are homologous, their amino acid or nucleotide sequences usually share significant identity

- Proteins that are homologous may be orthologous or paralogous

Orthologs = homologous sequences in different species that arose from a common ancestral gene during speciation

Paralogs = homologous sequences that arose by a mechanism such as gene duplication (may have different functions)

### Pairwise Alignment

- Assess the relatedness of any 2 proteins by performing a pairwise alignment (using BLAST) to achieve maximal levels of identity

- Percent similarity of 2 protein sequences is the sum of both identical and similar matches

- Pairwise alignment is useful to identify mutations that have occured during evolution

- Most common mututations = substitutions, insertions, deletions

### Accepted point mutation (PAM)

- Definition: A replacement of one amino acid in a protein by another residue that has been accepted by natural selection

- Abbreviated as PAM

- Amino acid change is accepted by natural selection occurs when:

	1. A gene undergoes a DNA mutation such that it encodes a different amino acid
	
	2. The entire species adopts that change as the predominant form of the protein
	
	
- Approach to define "accepted" mutations was based on a phylogenetic analysis

- Need to know the frequencies of occurence of each amino acid

- Dayhoff calculated the relative mutabilities of the amino acids - how often each amino acid is likely to change over a short evolutionary period

- Relative mutability: number of times each amino acid was observed to mutate by the overall frequency of occurence of that amino acid

Why are some amino acids more mutable than others?

- less mutable residues probably have important structural/functional roles in proteins so changing it could be harmful

- Use this data to generate a mutation probability matrix - each element of the Matrix shows the probability that an original amino acid j will be replaced by another amino acid i over a defined evolutionary interval

- For each original amino acid, it is easy to observe the amino acids that are most likely to replace it if a change should occur

- rows that have original amino acid, columns are replacement amino acids with scores

- Usefulness of PAM matrices by performing a series of global pairwise alignments of both closely related proteins and distantly related proteins

- EX: PAM250 matrix assumes the occurrence of 250 point mutations per 100 amino acids

- Twilight zone: A level of divergence, it is usually difficult to assess whether the two proteins are homologous.  Other techniques including multiple sequence alignment and structural predictions are useful to assess homology in these cases.'

### Types of Alignments 

- Global and local

- Global alignment: contains the entire sequence of each protein or DNA molecule

- Local alignment: focuses on the regios of greatest similarity between two sequences. Most database search algorithms such as BLAST use local alignments

### Global Sequence ALignment

- Algorithm for aligning two protein sequences --> produces an optimal alignment of protein or DNA sequences. 

- Result is optimal

- Needleman-Wunsch approach
	1. Setting up a matrix
	2. Scoring the matrix
	3. Identifying the optimal alignment
	
- BLAST was introduced as a local alignment search tool	
	


	

















