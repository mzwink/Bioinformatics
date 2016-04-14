#Inspecting and manipulating text data with unix
***
### *Unix pipelines entered directly into the command line provide a fast, low-level data manipulation toolkit to explore data, transform data between formats, and inspect data for potential problems*
***


##Inspecting data with head & tail
* #### The head command returns the first 10 lines of any data file, unless you specify otherwise with the -n option
`$ head Mus_musculus.GRCm38.75_chr1.bed`

	`$ head -n 3 Mus_musculus.GRCm38.75_chr1.bed`
* #### The tail command returns the *last* 10 lines of any data file, unless you specify otherwise with the -n option
`$ tail -n 3 Mus_musculus.GRCm38.75_chr1.bed`
* #### Putting both together allows you to look at the beginning and end at the same time
`$ (head -n 2; tail -n 2) < Mus_musculus.GRCm38.75_chr1.bed`
* ####You can combine head with the powerful grep to first search for a character string, perform a function on these data, but do so for only a specified number of times (i.e., head -n 5)
`$ grep "some_string" huge_file.txt | program1 | program2 | head -n 5`

##Inspecting data with less
###*Less is a terminal pager, a program that allows us to view large amounts of text in our terminals with some control over the data -- i.e., doesn't just fly by*


* ####Less is also a powerful way to examine output of programs in steps
`$ step1 input.txt | less` * This stops process after first step

	`$ step1 input.txt | step2 | less`

	`$ step1 input.txt | step2 | step3 | less`

##Data summary with wc, ls, awk
### *We may want information about the number of lines or characters in our file, the size of the file, or the number of columns in a file*  

* ####Use wc for counting words, lines, or characters, unless specified that you want only 1 of these options
	`$ wc Mus_musculus.GRCm38.75_chr1.bed`   

	`$ wc -l Mus_musculus.GRCm38.75_chr1.bed`
* ####Use ls for information about the size of a file  
	`$ ls -l Mus_musculus.GRCm38.75_chr1.bed`  

	`$ ls -lh *`  
	`$ ls -l *`
* #### Use awk to find out how many columns in a tab-delimited file  

	`$ awk -F "\t" '{print NF; exit}' Mus_musculus.GRCm38.75_chr1.bed`  

##Now we want to quickly convert our gtf file into a 3-column tab-delimited file of genomic ranges: use grep and cut together  
* ####First, take a look at the file Mus_musculus.GRCm38.75_chr1.gtf
* ####Use grep to pull out only lines without the first set of commented-out lines
* ####Next, pipe the output to the cut program to retain the 1st, 4th and 5th columns, and then to the head program to view *only* the first 3 lines   

	`$ grep -v "^#" Mus_musculus.GRCm38.75_chr1.gtf | cut -f1,4,5 | head -n 3`  
	`$ grep -v "^#" Mus_musculus.GRCm38.75_chr1.gtf | cut -f1,4,5 > test.txt`  


##Sort: We will want to work with sorted data to (1) speed up applications, (2) find unique lines, and (3) use the join command to join 2 datasets (very impt!!)  
* ####Do a simple sort on two columns
	`$ sort -k1,1 -k2,2n example.bed`
	
	`$ sort -k1,1 -k2,2n example.bed > example_sorted.bed`
* ####Is your file already sorted?
	`$ sort -k1,1 -k2,2n -c example.bed`
	
	`$ sort -k1,1 -k2,2n -c example_sorted.bed`
* ####Take a look at *how* sort is sorting
	`$ cat example2.bed`  
	
	`$ sort -k1,1 -k2,2n example2.bed`
* ####Let's fix that for our human brains
	`$ sort -k1,1V -k2,2n example2.bed`

 
##It's helpful to find *unique* values in files at a first-pass glance, and to be able to count the number of times a feature is repeated in a file. We do this using the unique command
* ####Do a comparison of all entries to those using the unique command
	`$ cat letters.txt`  
	`$ uniq letters.txt`
* ####Use unique and sort to count occurrences  
	`$ uniq -c letters.txt`  
	`$ sort letters.txt | uniq -c`
* ####Let's use these skills to summarize a bioinformatics dataset  
	`$ grep -v "^#" Mus_musculus.GRCm38.75_chr1.gtf | cut -f3 | sort | uniq -c`  

##Finally, we will often want to join 2 datasets that have a single column in common (ever done this in excel? Not fun!) 
* ####Take a look at the data  
	`$ cat example.bed`  
	`$ cat example_lengths.txt`
* ####To join them, *must* have both files sorted by the column in common  
	`$ sort -k1,1 example.bed > example_sorted.bed`  
	`$ sort -c -k1,1 example_lengths.txt` #shows that example_lengths is already sorted  
* ####Next, join the files  
	`$ join -1 1 -2 1 example_sorted.bed example_lengths.txt > example_with_lengths.txt`  
	`$ cat example_with_lengths.txt`  	
