The example underlying Figure 9-17 (on p.294-295) is a bit tricky. Let's take another look at it.
	
	> set.seed(0)
	> rngs <- IRanges(start=sample(seq_len(60),10),width=7)
	> rngs
	IRanges of length 10
     start end width
	[1]     54  60     7
	[2]     16  22     7
	[3]     22  28     7
	[4]     33  39     7
	[5]     51  57     7
	[6]     12  18     7
	[7]     49  55     7
	[8]     56  62     7
	[9]     35  41     7
	[10]    57  63     7
	> names(rngs)[9] <- "A"
	> rngs
	IRanges of length 10
     start end width names
	[1]     54  60     7  <NA>
	[2]     16  22     7  <NA>
	[3]     22  28     7  <NA>
	[4]     33  39     7  <NA>
	[5]     51  57     7  <NA>
	[6]     12  18     7  <NA>
	[7]     49  55     7  <NA>
	[8]     56  62     7  <NA>
	[9]     35  41     7     A
	[10]    57  63     7  <NA>
	> rngs_cov <- coverage(rngs)
	> rngs_cov
	integer-Rle of length 63 with 18 runs
	Lengths: 11  4  3  3  1  6  4  2  5  2  7  2  3  3  1  3  2  1
	Values :  0  1  2  1  2  1  0  1  2  1  0  1  2  3  4  3  2  1
 	 
There is a hidden sequence here, integer-Rle, of range 1 to 63. And it has 18 "runs"—places where one of our ranges (i.e., another sequence) overlaps integer-Rle. From base pairs 1-11 of integer-Rle, none of our ranges overlap, so the length=11 and the value=0. From base pairs 12-15 (the next four bases), one of our ranges ([6]) overlaps, so the length=4 and the value=1. From base pairs 16-18 (the next three bases), two of our ranges overlap ([2] and [6]), so the length=3 and the value=2. Keep going with this to figure out every position of integer-Rle that has an overlap with our ranges.

A real-world use for this is to ask how many times is each base of my reference genome "covered" by one of my sequence reads from my sequencing project. This is what is meant by the term "coverage".