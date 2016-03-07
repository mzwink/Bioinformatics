# Bioinformatics Data Skills 
## Chapter 3 

### Unix Shell

*cat* - will print out content of files (can print out multiple)

*> or >>* - A redirect operator, will redirect standard output to a file

*ls -lrt* 
	
	* ls will list files in a directory
	
	* -l is list format 
	
	* -r reverse 
	
	* -t time
	
*grep* - searches files or standard input for strings that match patterns

	* -c will count anything that matches pattern

	* -v will invert the matching lines 
	
	* To find any characters that are not A, T, G, or C:
			ex: grep --color -i "[^ATCG]"
			
	This will ignore case (-i), look for anything not match ATGC, and color the matching non-nucleotide characters
	
	
Can tell a program to run in the background with an ampersand (&)

- Example: $ program1 input.txt > results.txt &

fg will bring the process into the foreground again: 

	 $ fg

 	 program1 input.txt > results.txt
  
Exit Status

	$ program1 input.txt > results.txt
	
	$ echo $?
	
	0  
  
Exit statuses are useful because they allow us to programmatically chain commands together in the shell

*+%F* - tells the date program to output the date in a particular format.  Good for dated directories because when results are sorted by name, they are sorted chronologically.
	
	$ mkdir results-$(date +%F)
	
	$ ls results-2015-04-13
	
*alias* - simply aliases your command to a shorter name alias

	alias mkpr="mkdir-p {data/seqs,scripts,analysis}"
	
	alias today="date +%F"
	
		


  
  


	
	