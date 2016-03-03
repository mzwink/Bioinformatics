#Introduction to R Activity

###We want to analyze the recombination rates of named sequence motif repeats and compare between classes. Use the motif_recombrates.txt, the motif_repeats.txt, and the hotspot_motif.txt files to answer the questions below. Start a new Rproject in RStudio for this exercise. Note this exercise will require you to merge, summarize, subset, and plot data.

### 1. What is the average recombination rate per motif type?

	motifs: 	CCTCCCTAGCCAC 	CCTCCCTGACCAC
	Avg. Rate: 	
	
	

### 2. Do the distributions of recombination rate differ according to motif type? (You will need to make a plot using ggplot2 to answer this question).

	Plot is in Bioinformatics Folder

### 3. How do the recombination rates of the motif types differ from background (i.e., the recombination rate across all sequences; you will want to look at summary statistics and make a plot for this question).

	Find out how to do summary of the plot in 2

### 4. How many motif repeats are in motif hotspots?


	FALSE  TRUE 
	10832  9218 

### 5. How does the recombination rate of motifs in hotspots differ from motif repeats?



###Put your answers/plots in a pdf and email to me by Tuesday, March 8, 2016. Be sure to save your R code in an RMarkdown document or in a Mou Markdown document.


setwd("/Users/biology/Desktop/Bioinformatics_Zwink/bds-files-master/chapter-08-r/")
mtfs <- read.delim("motif_recombrates.txt", header=TRUE)
head(mtfs,3)
rpts <- read.delim("motif_repeats.txt", header=TRUE)
head(rpts, 3)
mtfs$pos <- paste(mtfs$chr, mtfs$motif_start, sep="-")
rpts$pos <- paste(rpts$chr, rpts$motif_start, sep="-")
head(mtfs, 2)
head(rpts, 2)
table(mtfs$pos %in% rpts$pos)
i <- match(mtfs$pos, rpts$pos)
mtfs$repeat_name <- rpts$name[i]
head(mtfs[!is.na(mtfs$repeat_name), ], 3)
mtfs_inner <- mtfs[!is.na(mtfs $repeat_name), ]
nrow(mtfs_inner)
recm <- merge(mtfs, rpts, by.x = "pos", by.y= "pos")
head(recm, 2)
recm <- merge(mtfs, rpts, by.x="pos", by.y="pos", all.x=TRUE)
p <- ggplot(mtfs, aes(x=dist, y=recom)) + geom_point(size=1)
library(ggplot2)
p <- ggplot(mtfs, aes(x=dist, y=recom)) + geom_point(size=1)
p <- p + geom_smooth(method="loess", se=FALSE, span=1/10)
print(p)
unique(mtfs$motif)
p <- ggplot(mtfs, aes(x=dist, y=recom)) + geom_point(size=1, color="grey")
p <- p + geom_smooth(method='loess', se=FALSE, span=1/10)
p <- p + facet_wrap(~ motif)
print(p)

recm <- merge(mtfs, rpts, by.x="pos", by.y="pos", all.x=TRUE)
head(recm, 3)

htspt <- read.delim("hotspot_motifs.txt", header=TRUE)
htspt$pos <- paste(htspt$chr, htspt$motif_start, sep="-")
table(htspt$pos %in% rpts$pos)
recm[ , c("motif","dist", "recom")]
recm_sub <- recm[ , c("motif","dist", "recom")]
head(recm_sub, 3)
table(mtfs$repeat_name, mtfs$motif, useNA="ifany")
table(mtfs$recom, mtfs$motif, useNA="ifany")
recm_sub <- recm[ , c("motif", "recom")]
summary(recm_sub)
recm_split <- split(recm_sub, list(recm_sub$motif))
summary(recm_split)


