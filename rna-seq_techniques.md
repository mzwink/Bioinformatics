#### RNA-seq Techniques

---


Overall:

	TopHat and Cufflinks are software tools for gene discovery and expression analysis of high-throughput mRNA sequencing (RNA-seq) data

	Allow biologists to identify new genes and new splice variants of known ones as well as compare gene and transcript expression under two or more conditions

CummeRbund

	Visualization of RNA-seq analysis
	
Process

	raw sequencing reads -> transcriptome assembly
	
	Lists of differentially expressed and regulated genes and transcripts and visualizations of analysis results
	
---

TopHat

	Aligns reads to the genome and discovers transcript splice sites
	
Cufflinks

	Uses this map against the genome to assemble the reads into transcripts
	
	Cuffdiff - a part of the Cufflinks package, takes the aligned reads from 2 or more conditions and reports genes and transcripts that are differentially expressed using a rigorous statistical analysis.
	
	CummeRbund - renders Cuffdiff output in figures and plots		
	
TopHat and Cufflinks require a sequenced genome

Can only be used with Illumina or SOLiD sequencing machines

---

Overview of Workflow:

goal - compare the transcriptome of wild-type vs. mutant 

Bowtie -> TopHat -> Cuffinks

1. Reads for each condition are mapped to the reference genome with TopHat

2. After running TopHat, resulting alignment files are provided to cufflinks to generate a transcriptome assembly for each condition

3. Assemblies are then merged together using the Cuffmerge utility which is included with the Cufflinks package

4. Reads and the merged assembly are fed to Cuffdiff which calculates expression levels and tests the statistical significance of observed changes

5. CummeRbund transforms Cufflinks output files into R objects suitable for analysis


	




