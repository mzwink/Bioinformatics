##Activity, February 25, 2016
__________________________________________________
  
####1. Using the Mus_musculus files, generate a file that lists chromosome number, geneid, gene name, start bp and end bp. (There are multiple ways this can be done -- use cut, sort, join, etc).

####2. Send this file to your instructor by Tuesday, March 1, 2016. This assignment will take the place of next week's quiz.

Mus_musculus bed file: Chromosome number --> start and end 
Mus_musculus gtf file: gene id, gene name, 

Chromosome number: Either bed or gtf
geneid: gtf
gene name: gtf
start and end: bed

To extract all values of the "gene_id" field

	$ grep -E -o 'gene_id "\w+"' Mus_musculus.GRCm38.75_chr1.gtf | head -n 5 gene_id "ENSMUSG00000090025"	gene_id "ENSMUSG00000090025"	gene_id "ENSMUSG00000090025"    gene_id "ENSMUSG00000064842"    gene_id "ENSMUSG00000064842"
    
Mus_musculus file 

- number ($1)

- gene id ($10)

- start ($4-1) - if using gtf

Use join to add the gene names to the file














    