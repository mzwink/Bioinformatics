###Fine-scale variation in meiotic recombination in Mimulus inferred from population shotgun sequencing


__Introduction:__

	Recombination - important in shaping genome-wide sequence variation
	
	- highly regulated, enables pairing of homologous chromosomes
	
	Strong recombination = hotspot
	
	Low recombination = cold spots
	
	Humans and mice: Regions of hotspots is determined by positive-regulatory domain zinc finger protein 9 (PRDM9)
	
	Yeast: regions associated with nucleosome-depleted open chromatin often associated with gene promoters
	
	When PRDM9 is disabled in mice, hotspots relocalize to promoter regions
	
	QUESTION: Tendency of hotspots in plants?
	
	 
_Why Mimulus guttatus?_

	Exceptionally high nucleotide diversity, ideal for characterizing the boundaries of recombination events
	
	Short-range haplotypes can be determined cost-effectively by shotgun sequencing pooled samples rather than by sequencing each plant individually
	
__Significance:__

	Characterizes variation in recombination across the genome of a flowering plant in detail using unique population genomic and computational approaches - advances understanding of basic properties of recombination near starts of genes, varying degrees of intensities of "hotspots", higher activity in exons than introns, and that a large fraction of the genome appears devoid of any recombination activity
		
	
__Results:__

	Sequenced pooled population samples of M. guttatus to an average of 255X genomic coverage using Illumina
	
	Reference genome sequence for M. guttatus was assembled for the IM62 line using conventional Sanger whole-genome shotgun methods
	
	To develop a collection of nearby segregating variants, identified all pairs of common, silent SNPs separated by 50 bp or less
	
	Normalized analysis to a sample size of 50 haplotypes per locus
	
_F4 Values:_
	
	F4 = fraction of such SNP pairs that have all four possible haplotypes represented in the dataset
	
	Found that the first coding exon of genes has highest F4 value
	
	Converted F4 values into recombination rate (p) = recombination boundaries per base per generation per haploid genome
	
	i. F4 depends on the minor allele frequency of the rarer SNP of the two sites (b/c rarer alleles usually arose recently, less time to participate in recomb events)
	
	ii. Distance between the two SNPs
	
	iii. Local recombination rate p
	
In this study, i and ii are known, so they could fit the local recomb rate p to F4 using a lookup table 

	This was based on observation that recombination rate is relative to the positions of genes
	
	To examine variation of recomb rate in and around genes, binned all nearby SNP pairs according to their position relative to individual exons and introns
	
	Crossover boundaries and/or the ends of gene conversion tracts tend to occur within exons rather than introns		

Local recomb rates vary across genome

	Analyzed sliding windows of 15 nonoverlapping pairs of SNPs and inferred the local recombination rate p as that which best matches the observed F4 according to the lookup table
	
	Found cold spots account for more than 25% of the sampled genome
	Remaining 75% exhibits varying degree of recombination
	
Overall find that hotspots tend to be located near start of genes and cold spots within genes
	
	Found about 13,000 hotspots
	Found 44,674 cold spots	

		 
	
__Figures__	
	
Figure 1

	Mutations and recombination producing more haplotypes
	
Figure 2
	
	Shows average F4 values as a funciton of distance to the nearest annotated coding DNA sequence (CDS)		
	
	Highest F4 values at 0 distance from nearest annotated coding sequence, drops off when moves farther away
	
	Suggests that the first coding exon of genes has on average nearly twice the amount of the recombination activity seen elsewhere
	
	*Start of genes have highest recomb rates (Polarity)
	
Figure 3

	F4 vs SNP separation for SNP pairs within 500 bp of CDS start
	
	F4 increases with distance between SNPs and with frequency of the least common allele

Figure 4

	Shows the results for genes with five or more exons	
	
	Average recomb rates are high in coding exons than in surrounding introns or UTRs
	
	Shows polarity
	
Figure 5

	Shows typical examples of the recombination landscape at two genomic scales	
	
__Discussion__	

	Overall, approach was applying the four gamete test to pairs of nearby SNPs that are spanned by multiple short-sequence reads, each read sampling a short-range haplotypes from the population
	
	Short reads - could results in possible msimapping-related artifacts
	
	Restricted analysis to reads with high mapping qualities
	
	Results:
	
	i. recomb events show polarity
	ii. a preference for the 5' end of genes
	iii. intron-exon dependence of recombination
	iv. Association of recombination hotspots with CpG islands
	
		
	
	
	
