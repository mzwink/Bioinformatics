#### April 19 Class 

_Running Transrate_

----

Learn about Transcriptome Assembly from Moreton Paper

Run transrate

	transrate --assembly NHAG-SOAPdenovo-Trans-assembly.fa --left NHAG-read_1.fq --right NHAG-read_2.fq.bz2
	
Output to Console

	[ INFO] 2016-04-19 14:23:23 : Calculating contig metrics...
	[ INFO] 2016-04-19 14:23:28 : Contig metrics:
	[ INFO] 2016-04-19 14:23:28 : 	-----------------------------------
	[ INFO] 2016-04-19 14:23:28 : n seqs                        51634
	[ INFO] 2016-04-19 14:23:28 : smallest                        100
	[ INFO] 2016-04-19 14:23:28 : largest                       13228
	[ INFO] 2016-04-19 14:23:28 : n bases                    31322882
	[ INFO] 2016-04-19 14:23:28 : mean len                     554.75
	[ INFO] 2016-04-19 14:23:28 : n under 200                   21243
	[ INFO] 2016-04-19 14:23:28 : n over 1k                     11085
	[ INFO] 2016-04-19 14:23:28 : n over 10k                        3
	[ INFO] 2016-04-19 14:23:28 : n with orf                    15065
	[ INFO] 2016-04-19 14:23:28 : mean orf percent              68.83
	[ INFO] 2016-04-19 14:23:28 : n90                             445
	[ INFO] 2016-04-19 14:23:28 : n70                            1016
	[ INFO] 2016-04-19 14:23:28 : n50                            1528
	[ INFO] 2016-04-19 14:23:28 : n30                            2128
	[ INFO] 2016-04-19 14:23:28 : n10                            4371
	[ INFO] 2016-04-19 14:23:28 : gc                             0.44
	[ INFO] 2016-04-19 14:23:28 : gc skew                         0.0
	[ INFO] 2016-04-19 14:23:28 : at skew                         0.0
	[ INFO] 2016-04-19 14:23:28 : cpg ratio                      1.63
	[ INFO] 2016-04-19 14:23:28 : bases n                       70926
	[ INFO] 2016-04-19 14:23:28 : proportion n                    0.0
	[ INFO] 2016-04-19 14:23:28 : linguistic complexity          0.12
	[ INFO] 2016-04-19 14:23:28 : Contig metrics done in 5 seconds

	[ INFO] 2016-04-19 14:31:39 : TRANSRATE ASSEMBLY SCORE     0.0269
	[ INFO] 2016-04-19 14:31:39 : -----------------------------------
	[ INFO] 2016-04-19 14:31:39 : TRANSRATE OPTIMAL SCORE       0.159
	[ INFO] 2016-04-19 14:31:39 : TRANSRATE OPTIMAL CUTOFF     0.0249
	[ INFO] 2016-04-19 14:31:39 : good contigs                  29123
	[ INFO] 2016-04-19 14:31:39 : p good contigs                 0.56


---

Assembly Score:

	Assembly socre allows you to compare two or more assemblies made with the same reads. Increased score is likely to correspond to an assembly that is more biologically accurate.
	
	0 = minimum possible socre
	1.0 = maximum
	
	More information in *assemblies.csv
	
	Contig scores and other metrics for each contig are saved in the *contigs.csv file for each assembly
	
Contig Scores:

	Used to filter out bad contigs from an assembly leaving only the well-assembled ones.
	
	The good contigs as determined by the cutoff optimisation procedure are output to the file good.*.fa
	
----		

RNA-Seq 

Index the Transcriptome

	bwa index -a is NHAG-SOAPdenovo-Trans-assembly.fa > bwa_index.stdout 2> bwa_index.stderr

Align read set 1 to the transcriptome

Created a SAM -> BAM

	ubuntu@54.186.117.117:~/IP_project$ samtools view -b NHAG.sam > NHAG.bam
	ubuntu@54.186.117.117:~/IP_project$ samtools flagstat NHAG.bam 
	7194 + 0 in total (QC-passed reads + QC-failed reads)
	0 + 0 secondary
	0 + 0 supplimentary
	0 + 0 duplicates
	6739 + 0 mapped (93.68%:-nan%)
	7194 + 0 paired in sequencing
	3597 + 0 read1
	3597 + 0 read2
	6473 + 0 properly paired (89.98%:-nan%)
	6579 + 0 with itself and mate mapped
	160 + 0 singletons (2.22%:-nan%)
	108 + 0 with mate mapped to a different chr
	91 + 0 with mate mapped to a different chr (mapQ>=5)
	
Missing the stats perl script
		
