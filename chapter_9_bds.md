### Chapter 9 BDS

Command line tools

	CrossMap
	
	NCBI Genome Remapping service
	
	LiftOver
	
Bioconductor core packages

	GenomicRanges
	
	Genomic Features
	
	Biostrings and BSgenome
	
	rtracklayer
	
[Bioconductor Documentation](http://bioconductor.org)

Bioconductors IRanges package: Implements data structures for generic ranges and sequences as well as the necessary functions to work with these types of data in R


---

__IRanges__

	1-based systems

	IRanges can also take vector arguments
	
	Can also create plots with plotIRanges()
	
	Ranges can also be merged with function c()
	
To move up or downstream kilobases, use L:
	
	> x <- IRanges(start=c(40,80), end=c(67,114))
	> x + 4L
	IRanges of length 2
   	 start end width
	[1]    36  71    36
	[2]    76 118    43
	
Can restrict ranges within a certain bound:

	restrict() cuts a set of ranges such that they fall inside of a certain bound
	
	> y <- IRanges(start=c(4,6,10,12), width=13)
	> y
	IRanges of length 4
    	start end width
	[1]     4  16    13
	[2]     6  18    13
	[3]    10  22    13
	[4]    12  24    13
	> restrict(y, 5, 10)
	IRanges of length 3
    	start end width
	[1]     5  10     6
	[2]     6  10     5
	[3]    10  10     1
	
The flank function returns the regions that flank each range in an IRanges object:

	> x
	IRanges of length 2
    	start end width
	[1]    40  67    28
	[2]    80 114    35
	> flank(x, width=7)
	IRanges of length 2
    	start end width
	[1]    33  39     7
	[2]    73  79     7
	
	Useful in creating ranges upstream and downstream of protein coding genes that could contain promoter sequences 
	
	By default, flank() creates ranges width positions upstream of the ranges passed to it
	
Flanking ranges downstream can be created by setting start = FALSE:

	> flank(x, width=7, start=FALSE)
	IRanges of length 2
   		start end width
	[1]    68  74     7
	[2]   115 121     7
	
The reduce operation:

	Any overlapping ranges are merged into a single range in the result
	
	
	> head(alns, 4)
	IRanges of length 4
   	 start end width
	[1]    45  49     5
	[2]    14  18     5
	[3]    18  22     5
	[4]    27  31     5
	> reduce(alns)
	IRanges of length 3
   	 start end width
	[1]     3  22    20
	[2]    24  36    13
	[3]    40  53    14	
	
Similar to reduce is gaps:

	returns the gaps between ranges 
	
	Useful for creating intron ranges between exon ranges, finding gaps in coverage, defining intragenic regions betweeen genic regions
	
	> gaps(alns)
	IRanges of length 2
    	start end width
	[1]    23  23     1
	[2]    37  39     3	
	
Can specify the start and end of the sequence:	

	gaps(alns, start=1, end=60)
	
Other useful functions:

	intersect()
	union()
	setdiff()	
	
Finding overlaps between two sets of IRanges objects using the findOverlaps() function:

	Takes query and subject IRanges objects as its first two arguments 
	
	Returns an object with class Hits and stores these overlaps
	
	can use type "within" or "any"
	
Use NCList instead of IntervalTree:

	A data structure that exploits the property of naturally ordered ranges along a sequence so we can avoid having to check if each of our Q query ranges overlap our S subject ranges
	
	Most appropriate for tasks that involve finding overlaps of many query ranges against a fixed set of subject ranges
	
	Can build the subject interval tree ibce abd tgeb we can use it over and over again when searching for overlaps with each of the query ranges	
		
Operations that focus on finding ranges that neighbor query ranges:

	nearest(): Returns the nearest range, regardless of whether it's upstream or downstream of the query
	precede()
	follow()		
	Both of these functions return the nearest range that the query and subject ranges as their first and second arguments, and return an index to which subject matches
	
_Other similar functions_ 

distanceToNearest() and distance():
	
	> distanceToNearest(qry, sbj)
	Hits object with 5 hits and 1 metadata 	column:
    	  queryHits subjectHits |  distance
      	<integer>   <integer> | <integer>
  		[1]         1           5 |        79
  		[2]         2           5 |        57
  		[3]         3           1 |        46
  		[4]         4           5 |       207
  		[5]         5           3 |       102

	Distance returns pairwise distances
	
	> distance(qry, sbj)
	[1] 500 538 188 258 731
	
Run-length encoding and coverage():

	> x <- as.integer(c(4,4,4,3,3,2,1,1,1,1,1,0,0,0,0,0,0,0,1,1,1,4,4,4,4,4,4,4))
	> xrle <- Rle(x)
	> xrle
	integer-Rle of length 28 with 7 runs
  	Lengths: 3 2 1 5 7 3 7
  	Values : 4 3 2 1 0 1 4	
  	
  	Can make this list a vector and run arithematic on the data
  	
The function slice takes a run-length encoded numeric vector as its argument and slices it, creating a set of ranges wehre the run-length encoded vector has some minimal value

	Can summarize views using viewMeans(), viewMaxs(), and viewApply()  
	
__Storing Genomic Ranges with GenomicRanges__

GenomicRanges package introduces a new class called GRanges for storing genomic ranges			
