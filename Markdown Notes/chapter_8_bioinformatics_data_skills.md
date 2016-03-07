## Chapter 8 Bioinformatics Data Skills

### R Language

getwd()
	
	Use to print out R's current working directory 
	>getwd()
	[1] "/Users/vinceb"
	
setwd()	
	
	Uset this to set the working directory
	>setwd("~/bds-files/chapter-08-r")
	
Inspect the file from the command line before loading into R to see which column delimeter is being used

	$ head -n 3 Dataset_S1.txt
	
	Can see that it is separated by commas
	
Once working directory is set, load data into R

	read.csv() <-- Reads CSV
	
	read.delim() <-- Reads tab-delimited files
	
	>d <- read.csv("Dataset_S1.txt")
	Using d to assign the variable so that we won't have to type out a long name each time
	

read.csv() and read.delim() have argument header set to TRUE by default. Some data files don't include a header so you need to set header = FALSE

	For example: loading a tab-delimeted file named noheader.bed contains three columns named chrom, start, and end
	
	>bd <-- read.delim("noheader.bed", header=FALSE, col.names=c("chrom", "start", "end"))		
	
	col.names argument is used to assign column names 
	
Commonly used read.csv() and read.delim() arguments

	header: A TRUE/FALSE value indicating whether the first row contains column names rather than data
	
	sep: A character value indicating what delimits columns; using the empty string "" treats all whitespace as a seperator
	
	stringAsFactors: Setting this argument as FALSE prevents R from coercing character vectors to factors for all columns; see argument asis in help(read.delim) to prevent coercion to factor on specific columns
	
	col.names: A character vector to be used as column names
	
	row.names: A vector to use for row names, or a single integer or column name indicating which column to use as row names
	
	na.strings: A character vector of possible missing values to convert to NA
	
	colClasses: A character vector of column classes; "NULL" indicates a column should be skipped and NA indicates R should infer the type 
	
	comment.char: Lines beginning with this argument are ignored; the empty string disables this feature
	
Reading and loading the data stores it as a dataframe and consists of columns and rows.

Arguments to see how data is organized in the dataframe:
	
	>head(d, n=3)
	Limits to the first 3 lines being shown (default is 6)
	
	Number of rows: 					Row names:
	> nrow(d)							> rownames(d)
	
	Number of columns:					Column names:					
	> ncol								> colnames(d)
	
	Dimensions(returns both):			Colunm depth:
	> dim(d)							> d$depth
	
With the depth column argument, we can use the mean() or summary() to get an idea of what depth looks like across this dataset

To look at specific columsn and rows, we can use:

	> d[ , 1:2] OR > d[, c("start", "end")]
	
	Can get only first row of start and end positions by:
	
	> d[1, c("start", "end")]	
	
	Single cells can be accessed by specifying a single row and a single column
	
	> d[2,3]
	
When accessing a single column from a dataframe, R's default behavior is to return this as a vector - not a dataframe with one column. To disable this, you can use:

	> d[, "start", drop=FALSE]
	
If we want an additional column to our dataframe that indicates whether a window is in the centromere region (chromosome 20 = 25,800,000-29,700,000) we can append to our d dataframe a column called *cent* that has TRUE/FALSE values

	> d$cent <- d$start >= 25800000	 & d$end <=29700000
	* Use logical operators			
	
	> table(d$cent)
	This will give us the number of TRUE and FALSE values
	
	> sum(d$cent)
	This will give the sum as FALSE = 0 and TRUE =1
	
Most powerful feature of dataframes is the ability to splice out specific rows by applying the same vector subsetting techniques 

Using comparison and logical operators, we can query out rows in a dataframe

Subset Argument

	subset()
	
	> $ subset(d, Pi > 16 & X.GC > 80)
	
	Instead of 
	
	> d[d$Pi > 16 & d$X.GC > 80, ]
	
	Can also specify which column and in what order to include:
	
	> $ subset(d, Pi > 16 & X.GC > 80, c(start, end, Pi, X.GC, depth))
	* Don't need to quote column names with this argument
	
### VISUALIZING DATA

Graphing using the "ggplot2" because it is simple and useful for creating complex graphs

Because our data is window based, need to add a column called position that is midpoint between each window

	> d$position <- (d$end + d$start) / 2
	> ggplot(d) + geom_point(aes(x=position, y=diversity))
	
There are 2 componenets of this ggplot2 graphic: the call to the fucntion ggplot() and the call to the function geom_point()

	1. ggplot(d) to supply this plot with our d dataframe
	
	2. With our data specified, we then add layers to our plot (+ operator). Each layer updates our plot by adding geometric objects such as the points in a scatterplot or the lines in a line plot
	
ggplot has many geoms (e.g. geom_line(), geom_bar(), geom_density(), geom_boxplot(), etc.)

We specify the mapping of aesthetic attributes to the columns in our dataframe using the function aes()

To change axis labels, plot titles, and scales:

	xlab() - x axis
	ylab() - y axis
	ggtitle() - plot title
	
	For example:	
	p + xlab("chromosome position(basepairs)" + ylab("nucleotide diversity"))
	
	Can also set limits for continuous axes using the function 
	scale_x_continuous(limits=c(start, end))	
	AND
	scale_y_continuous()
	
	Similarly:
	scale_x_log10() AND scale_y_log10()	
	
The simplest opertaion to match two vectors is checking whether some of a vector's values are in another vector using R's %in% y returns a logical vector indicating which of the values of x are in y 

	> c(3, 4, -1) %in% c(1, 3, 4, 8)
	[1] TRUE TRUE FALSE
	
	> match(c("A", "C", "E", "A"), c("A", "B", "A", "E"))	[1] 1 NA 4 1
	
	* Gives the position of the match in y	
	
### Merging and Combining Data

1. Load in both files

2. Consider the structure of both and find the link between these 2 datasets

		Example:
		
		> mtfs$pos <- paste(mtfs$chr, mtfs$motif_start, sep="-")
		> rpts$pos <- paste(rpts$chr, rpts$motif_start, sep="-")
		
3. Validate that your keys overlap in the way you think they do before merging

		> table(mtfs$pos %in% rpts$pos)
		FALSE	TRUE
		10832	9218
		
		This means there are 9,218 motifs in mtfs with corresponding entry in rpts and 10,832 without
		
		Remember that directionality matters with %in% function
		
4. Now we use match() to find where each of the mtfs$pos keys occur in the rpts$pos

		> i <- match(mtfs$pos, rpts$pos)
		>table(is.na(i))
		FALSE	TRUE
		9218	10832
		
5. Using this index vector we can select ourt the appropriate elements of rpts $name and merge these into mtfs:

		> mtfs$repeat_name <- rpts$name[i]
		
		Often in practice you might skip assigning match()'s results to i and use this directly:
		
		> mtfs$repeat_name <- rpts$name[match(mtfs$pos, rpts$pos)]		
		
Merging data is tricky so we can look at some rows where mtfs$repeat_name isn't NA and check with the UCSC Genome Browser

	> head(mtfs[!is.na(mtfs$repeat_name), ],3)	
	
R does have a more user-friendly merging function: merge(). Merge can directly merge two datasets:

	>recm <- merge(mtfs, rpts, by.x="pos", by.y="pos")
	
	merge() takes two dataframes x and y and joins them by the columns supplied by by.x and by.y
	If they aren't supplied merge() will try to infer what these columns are but it's much safer to supply them explictly
	Acts like match() by default
	
### Using ggplot2 Facets

Facets allow us to visualize grouped data by creating a series of separate adjacent plots for each group

	> p <- ggplot(mtfs, aes(x=dist, y=recom)) + geom_point(size=1)
	> p <- p + geom_smooth(method="loess", se=FALSE, span=1/10)
	>print(p)
	
Use faceting to pick the data apart

ggplot2 has two facet methods: facet_wrap() and facet_grid():

	facet_wrap() takes a factor column and creates a panel for each level and wraps around horizontally 
	
	facet_grid() allows finer control of facets by allowing you to specify the columns to use for vertical and horizontal facets
	
For Example:

	> ggplot(mtfs, aes(x=dist, y=recom)) + geom_point(size=1) + geom_smooth(aes(color=motif), method="loess", se=FALSE, span=1/10)
	> p <- ggplot(mtfs, aes(x=dist, y=recom)) + geom_point(size=1, color="grey")
	> p <- p + geom_smooth(method='loess', se=FALSE, span=1/16)
	> p <- p + facet_grid(repeat_name ~ motif)
	> print(p)
	
	The tilde(~) used with facet_wrap() and facet_grid() is how we specify model formula in R
	By default, x- and y-scales will be the same across all panels
	You can set scales to be free with scales="free_x" and scales="free_y"
					
The list function: list()

Lists are like vectors but can have multiple types of structures in it

We can create lists with this function and useful if we want to store a specific genomic position:

	> adh <- list(chr="2L", start=14615555L, end=14618902L, name="Adh")
	> adh
	
	This will print out all the values associated with adh
	If we tried to store this in a vector, vector coercion would coerce them into a character vector
	
The string function: str()

str() prints a line for each contained data structure, complete with its type, length, and the first few elements it contains

	> z <- list(a=list(rn1=rnorm(20), rn2=rnorm(20)), b=rnorm(10))
	> str(z)
	List of 2
	Will print out the contained data structre
	
Similar to vectors, list names can be accessed with names() or changed using names(x) <-
			
### Writing and Applying Function to lists wtih lapply() and sapply()

Using lapply()

	> lapply(ll, mean)
	
	This will return the mean for each row as a list

R's parallel package has a prallelized drop-in verion of lapply() called mclapply() ("mc" stands for multi-core)

### Writing functions in R

We can write a simple version of R's mean() function with na.rm = TRUE:

	> meanRemoveNA <- function(x) mean(x, na.rm=TRUE)
	> lapply(ll, meanRemoveNA)
	
Syntax for meanRemoveNA() is a common shortened version of the general syntax for R functions:
	
	fun_name <- function(args){
		# body, containing R expressions
		return(value)
		}
		
To create polished functions such as constructing a meanRemoveNAVerbose() function, we specify that the argument warn is TRUE by default in the arguments:

	meanRemoveNAVerbose <- function(x, warn=TRUE){
		# A function that removes missing values when calculating the mean
		# and warns us about it
		
		if (any(is.na(x)) && warn){
			warning("removing some missing values!")			
			}
		mean(x, na.rm=TRUE)
		}
		
		
Don't try to type these out directly in the R interpreter: functions over one line should be kept in a file and sent to the interpreter. Rstudio conveniently allows you to send a whole function definition at once with Command-Option-f on a Mac

Function Scope


One of the benefits of using functions in your code is that they organize the code into separate units. One way functions separate code is through *scoping* which is how R's functions finds the values of variables. The limited scope of R's functions prevents mistakes due to name collisions.

	> x <- 3
	> fun <- function(y) {
		x <- 2.3
		x + y
	  }
	> fun(x)
	[1] 5.3
	> x
	[1] 3
	
	Value of x outside of the scope is not changed.
	
Use browser() to step through a function one line at a time to help debug
Useful to see how variables change throughout the function

sapply():

sapply() can simplify more complex data structures than this simple list

	> sapply(ll, function(x) mean(x, na.rm=TRUE))
	
mapply():

multivariate version of sapply(). Can take in and use multiple arguments. Example, suppose you had 2 lists of genotypes and you wanted to see how many alleles are shared by calling intersect() pairwise on both lists

First argument is the function you want to apply

Then takes as many vectors as there are needed arguments in the function applied to the data		

	> ind_1 <- list(loci_1=c("T", "T"), loci_2=c("T", "G"), loci_3=c("C", "G"))
	> ind_2 <- list(loci_1=c("A", "A"), loci_2=c("G", "G"), loci_3=c("C", "G"))
	> mapply(function(a, b) length(intersect(a,b)), ind_1, ind_2)
	
	loci_1	loci_2	loci_3
		0		1		2
		
		
split():

Splitting data combines observations into groups based on levels of the grouping factor

We split a dataframe or vector using split(x, f) where x is a dataframe/vector and f is a factor

With out data split into groups, we can then apply a function to each group using the lapply() function we learned earlier

unlist():

returns a vector with the highest type it can 

do.call():

It constructs and executes a function call. Function calls have two parts: the name of the function you're calling and the arguments supplied to the function

	
	> func(arg1, arg2, arg3)
	
	> do.call(func, list(arg1, arg2, arg3))			  
		
	Example:
	> do.call(rnorm, list(n=4, mean=3.3, sd=4))
	
tapply() and aggregate() can be used to create per-group summaries. Both have the same split-apply-combine pattern at their core, but vary slightly in the way they present their output.


### Exploring Dataframes with dplyr

dplyr uses a simple class called tbl_df that wraps dataframes so that they don't fill your screen when you print them (similar to head())

	> d_df <- tbl_df(d)
	
Then you can print the selected columns from d_df using select() functions
	
	> select(d_df, start, end, Pi, Recombination, depth)
	This is the equivalent of d[, c("start", "end", "Pi", "Recombination", "depth")]
	
filter():

This is similar to subsetting dataframes using expression with logical and comparative operators 

	> filter(d_df, Pi>16, X.GC > 80)		
	

arrange():

You can sort a column in descending order using arrange() by wrapping its name in the function desc()
	
mutate():

We can add new columns to our dataframe

mutate() creates new columns by transforming existing columns 

	
	
		

	
							
	

		
				
		

	
	


	
	
			

