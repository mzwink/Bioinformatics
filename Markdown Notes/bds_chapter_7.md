## Bioinformatics Data Skills Chapter 7 

### Unix Data Tools


Connecting tools together to create programs from Unix pipelines

Unix pipelines can be developed in shell scripts as "one liners"









This is not appropriate for all problems

Storing pipelines in scripts is a good approach - not only do scripts serve as documentation of what steps were performed on data, but they allow pipelines to be rerun and can be checked into a Git repository

#### Working with Text Files

Tab-delimited or comma-separated format (CSV)

Using head is useful to see if there are column headers and how many columns there are as well as what delimeter is being used.

Can use tail to remove the header of a file

	$ seq 3 > nums.txt
	$ cat nums.txt
	
	$ tail -n +2 nums.txt
	
	Tail will start from the xth line. So to chop off the header, we start from the second line with -n +2
	
less allows us to view and scroll through long files and standard output a screen at a time		

Also helpful with pipelines to inspect output

	$ step1 input.txt | less 
	$ step1 input.txt | step2 | less





If we only care about the number of lines, we can use option -l 

	$ wc -l Mus_musculus.GRCm38.75_chr1.bed 81226 Mus_musculus.GRCm38.75_chr1.bed


	$ awk -F "\t" '{print NF; exit}' Mus_musculus.GRCm38.75_chr1.bed 3
	
-F argument changes field separators to just tabs

Using tail is not the best solution for getting rid of the file because you need to know how many lines to remove which is specific to each file (hardcoding)

Simple solution is to exclude all lines that match a comment line pattern by using grep

	$ grep -v "^#" Mus_musculus.GRCm38.75_chr1.gtf | head -n 3
	1 unprocessed_pseudogene exon 3054233 3054733 . + . [...]
	
cut - program cuts out specified columns (fields) from a text file

	$ cut -f 2 Mus_musculus.GRCm38.75_chr1.bed | head -n 3 3054233











1. The pattern - string or basic regular expression you want to search for

2. The file (or files) to search for it in 



Example: suppose you wanted a list of all genes that contain "Olfr" except "Olfr1413"

	$ grep Olfr Mus_musculus.GRCm38.75_chr1_genes.txt | grep -v Olfr1413
	
-w option matches entire words (surrounded by whitespace); by constraining our matches to be words, we're using a more restrictive pattern

If we want to find the Ensembl gene identifiers for both "Olfr1413" and "Olfr1411" we could use:

	$ grep "Olfr141[13]" Mus_musculus.GRCm38.75_chr1_genes.txt 			ENSMUSG00000058904 Olfr1413



-c option to count how many lines match a pattern

	$ grep -c "\tOlfr" Mus_musculus.GRCm38.75_chr1_genes.txt
	
We could also pipe the matching lines to wc -l:

	$ grep "\tOlfr" Mus_musculus.GRCm38.75_chr1_genes.txt | wc -l
	
To look at a file's encoding use the program file

	$ file Mus_musculus.GRCm38.75_chr1.bed Mus_musculus.GRCm38.75_chr1.gtf	
	
		
_sort_

Designed to work with plain-text data with columns. Running sort without any arguments simply sorts a file alphanumerically by line

	$ sort example.bed 
	chr1 10 19 
	chr1 26 39 
	chr1 32 47 
	chr1 40 49 
	chr1 9 28 
	chr2 35 54 
	chr3 11 28 
	chr3 16 27		
Because chromosome is the first column, sorting by line effectively groups chromosomes together in sorted order

But we want to use new features 

- Ability to sort by particular columns

- Ability to sort that certain columns are numberic values not alphanumeric text

To sort by chromosome (first column) and start position (second column):

	$ sort -k1,1 -k2,2n example.bed 
	chr1 9 28
Here we specify the columns and their order and we want to sorty by as -k arguments (-k specifies the sorting keys and their order) and -k,2n says sort numerical data

End result is that rows are sorted by chromosome and start position so we can redirect the output to a file 

	$ sort -k1,1 -k2,2n example.bed > example_sorted.bed
	
	
If you need all columns to be sorted numerically, can use -n rather than 2n

Sorting Stability:

	When lines are equivalent, sort will sort them according to the entire line as a last-resort effort to put them in some order. If we don't want sort to change the order of lines that are equal according to our sort keys, we can specify the -s option which turns off this last-resort sorting making it a stable sorting algorithm
	
	
We can check if a file is already sorted according to our -k arguments using -c

	$ sort -k1,1 -k2,2n -c example_sorted.bed
	$ echo $?
	0
	
	
0 means that it is already sorted - TRUE

1 means that it is out of order - FALSE

To sort in reverse, use -r argument. Can also append r on that column's -k argument

	$ sort -k1,1 -k2,2nr example.bed
	
	



Sort uses MergeSort

_uniq_ 

Takes lines from a file or standard input stream and outputs lines with consecutive duplicates removed

	$ cat letters.txt 
	A

uniq only removes consecutive duplicate lines (keeping one). If we want to find all unique lines in a file, we sort all lines sort so that all identical lines are grouped next to each other, then run uniq

	$ sort letters.txt | uniq 	
	A







Goal is to append the chromosome length alongside each feature - need to join both of these tabular files by their common column (chromosome names)

First, we need to sort both files by the column to be joined on:

	$ sort -k1,1 example.bed > example_sorted.bed

Use join Syntax: join -1 <file_1_field> -2 <file_2_field> <file_1> <file_2>

	chr3 11 28 24859




	Automatically assigns the entire record to the variable $0 and field one's value is assigned to $1, field two's value is assigned to $2 ...
	
Each pattern is an expression or regular expression pattern.

Patterns are a lot like if staments in other languages: if the pattern's expression evaluates to true or the regular expression matches, the statements inside action are run 

	$ awk '{ print $0 }' example.bed
	chr1 	26 		39



We can also chain patterns, by using logical operators && (AND), || (OR), and ! (NOT). For example, if we wanted all lines on chromosome 1 with a length greater than 10:






	toupper(s)	Convert string s to uppercase
	substr(s, i, j)	Return the substring of s that starts at i and ends at j
	split(s, x, d)	Split string s into chunks by delimiter d, place chunks in array x
	sub(f, r, s)	Find regular expression f in s and replace it with r
	
	
__Bioawk: An Awk for Biological Formats__

Can serve as a method of counting the number of FASTQ/FASTA entries

Bioawk's function revcomp() can be used to reverse complement a sequence

Two options that make working with plain tab-delimited files easer

	-t: for processing general tab-delimited files, sets Awks field separator (FS) and output field separator (OFS) to tabs
	
	-c hdr: unspecified tab-delimited formats with a header as the first line
	
	








		


	
