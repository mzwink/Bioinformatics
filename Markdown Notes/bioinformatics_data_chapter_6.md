## Bioinformatics Data Chapter 6

#### _wget and curl_

#### wget

Downloading a file to current directory:

	wget http://hgdownload.soe.ucsc.edu/goldenPath/hg19/chromosomes/chr22.fa.gz
	
	* Don't need authentication becasue UCSC provides human reference genome publicly
	
Some HTTP or FTP need authentication, you can authenticate using:

	--user = AND --ask-password options
	
	
wget can download data recursively

	--recursive OR -r	
	
	
Recursive downloading can be useful for downloading all files of a certain type from a page. 

Example:

	$ wget --accept "*.gtf" --no-directories --recursive --no-parent http://genomics.someuniversity.edu/labsite/annotation.html		
	
If recursive is not restrained, it will download everything it can reach within the maximum depth set by -- level

#### curl

curl behaves similarly to wget but by default writes the file to standard output

	curl http://hgdownload.soe.ucsc.edu/goldenPath/hg19/chromosomes/chr22.fa.gz > chr22.fa.gz
	
	
If you do not want to redirect curl's output, use -O <filename> to write the results to <filename>

Advantages of curl: 

- It can transfer files using more protocols than wget including SFTP (secure FTP) and SCP (secure copy). 
	
- It can follow page redirects if the -L/--location option is enabled. It will download the ultimate page the link redirects to, not the redirect page itself	


wget and curl are appropriate for quickly downloading files from the command line, but not optimal for some heavier duty tasks

#### Rsync and Secure Copy 

Better tool for synchronizing entire directories across a network is Rsync

Rsync is often faster because it only sends the _difference_ between file versions and can compress files during transfers

Also has an archive option that preserves links, modification timestamps, permissions, ownership, and other file attributes - good choice for network backups of entire directories

Syntax is rsync source destination where source is the source of the files or directories you want to copy, destination is the destination you'd like to copy these files to

	user@host:/path/to/directory/.
	
	$ rsync -avz -e ssh zea_mays/data/ vinceb@[...]:/home/deborah/zea_mays/data	
	
Trailing slashes means copy the entire directory itself, no trailing slash means the directory didn't already exist on the remote destination host

Secure copy is perfect for quickly copying a single file over SSH. Works like cp except we need to specify both host and path

	$ scp Zea_mays.AGPv3.20.gtf 192.168.237.42:/home/deborah/zea_mays/data/	
	
Looking at Differences Between Data

Unix tool diff - works line by line

	$ diff -u gene-1.bed gene-2.bed
	
Data Compression

Condensing data so that it takes up less space - compression ratio about 2.95 and saves about 66% space

gzip - compresses and decompresses data

With the imaginary program that removes low quality bases from FASTQ files

	$ trimmer in.fastq.gz | gzip > out.fastq.gz
	
	gzip takes input from standard in, compresses it, and writes this compressed output to standard out
	
We can also decompress files

	$ gunzip in.fastq.gz 
	
	Append .gz to the orignal filename
	
Both gzip and gunzip can also output their results to standard out using -c option

	$ gzip -c in.fastq > in.fastq.gz
	$ gunzip -c in.fastq.gz > duplicate_in.fastq
	
Redirect option is >> and overwrite option is >

zgrep and zcat handle compressed input and pipe output directly to the standard input of another program

	$ zgrep --color -i -n "AGATAGAT" Csyrichta_TAGGACT_L008_R1_001.fastq.gz
	2706: ACTTCGGAGAGCCCATATATACACACTAAGATAGATAGCGTTAGCTAATGTAGATAGATT			

