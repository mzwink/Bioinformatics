#### Rapid evolution and gene expression: A rapidly-evolving Mendelian trait that silences field crickets has widespread effects on mRNA and protein expression

_linking phenotypic evolution with genomic changes_


Generic evolutionary research question: 
	
	How novel sequence variants arise within a genome and persist or spread under selection
	
	Want to look at the genomics of rapidly evolving mutations
	
	
Goal of Research:

	To qualitatively test the universality of effects on gene expression caused by the flatwing mutations in developing bud tissue	

	
Looking at a mutant form of silent male crickets that has recently arisn and rapidly spread in several populations, apparently in response to pressure from an acoustically-orienting parasitoid fly
	
	Mutation = flatwing and is sex-specific (affects male forewings)
	
	Appeared only a decade ago but now there are distinct forms that segregate as sex-linked, sex-limited Mendelian traits in each
	
	Advantage of mutation = protects males from parasitiod attack
	
	Disadvantage of mutation = impedes their ability to attract females
	but females still accept silent males- mutation rapidly spread
	
Methodology:

	Used data from RNA and protein expression screens 
	
Steps:

1. Characterized the wing bud transcriptome and quantitatively compared gene expression profiles between wild-type and flatwing male wing buds

2. Similarly accessed the wing bud proteome and quantitatively compared protein expression patterns between wild-type and flatwing male wing buds

3. Established patterns of co-expression between the datasets levels to gain focused information about the molecular basis of the flatwing phenotype

4. Used existing information from D. melanogaster to test predictions about wing vein pathways implicate in the development of flatwing morphology in T. oceanicus	


Set-Up:

- Homozygous lines for each morph were done with 30 replicates of each of the types of crosses

- Selected 3 of the homozygous wild-type lines to retain for a total of 3 biological replicates of each genotype

- Interest in patterns of gene expression in wing buds when they appear externally


RNA extractions:

- purification kit

- 12 wing bud tissue samples were analysed

- purified RNA was converted to cDNA and purified 

- Used illumia for sequencing

RNA-seq data analysis:

- Produce samples in fastq format and trimmed to remove adapter sequences and low quality bases removed using Sickle (min score of 20) 

Transcriptome assembly:

- Assembled using Trinity

- RSEM was used for quantifying transcript abundances

- Used BOWTIE2 to map the trimmed illumina reads to the _de novo_ transcriptome

- BAM files used to generate raw couts for differential expression analysis

- EdgeR was used for identifying genes and isoforms differentially expressed between wild-type vs. flatwing

Quantitative Proteomics:

- Huh????

MS/MS data analysis:

- Searched against the NCBInr database

- Searches were performed against a wing bud transcriptome database



_Comparison between RNA-seq and proteomics datasets were evaluated to estimate patterns of expression in the transcriptome versus in the proteome_

Lastly, implemented a candidate gene detection test to evaluate the hpothesis that coding genes implicated in Drosophila wing development and venation also underlie similar developmental processes in T. oceanicus

AND, that the flatwing mutation causes expression levels of those genes in the male wing buds to be disrupted 

Test to see whether transcriptome and proteome expression profiles were consistent w/ disruption of nay of these during the develop;ment of flatwing morphology

---

__Results__

- Majority of genes were present (98%) but 79% was complete

- 2341 differentially expressed (DE)assembled sequences were identified therefore potentially involved in pathways leading to development of the flatwing phenotype

		Down-regulation = prevalent in flatwing males
		
		1716 were down regulated
		625 up-regulated
		
- 21% of DE sequences had annotation

- Most genes would be predicted to be involved in development of the flatwing phenotype based on known role in other insects

- Found the _protein white_, involved in male courtship behavior was up-regulated in flatwings


- vacuolar sorting-associated protein assigned to social behavior was also up-regulated

- down-regulated: protein linked to flight behavior, sperm aster formation and cuticle pigmentation

__Transcriptome and proteome correlation:__

- 9 DE assembled transcripts were identified in the wing bud proteome and from these only 5 were differentially expressed in both datasets

- For these, the magnitude of differential expression was more extreme at the transcriptome level than at the proteome level

- From the candidate gene detection test, about 30% of the Drosophila wing development genes were identified in the cricket wing bud transcriptome, but only 10% were DE

- Confirms that few known candidate wing development and wing venation genes appear to be differentially epxressed bewteen wild-type and flatwing crickets at the wing bud stage studied

---

__Discussion__


Flatwing mutation is associated with a broad spectrum of effects on mRNA and protein expression in developing male wing buds

1. Signatures of flatwing-associated effects on several biological processes

2. Evidence that endocrine disruption may contribute to the feminised wing phenotype

3. Prevalent down-regulation of transcrript expression in flatwing males' wing buds

4. Candidate genes for Drosophila wing morphogenesis represented, but mostly not differentially-expressed, in the cricket transcriptome

5. Differences in patterns of gene expression at the transcriptome versus proteome level, but commonality of some functional pathways

Results suggest an interesting pattern of lower transcriptional variation in flatwing crickets than in wild-type crickets, particularly when looking at the DE transcripts that maximize differences between morphs

Found that locomotion, circadian rhythm and signalling were consistently down-regulated in flatwings

Some of the most interesting genomic functions recovered were not related to wing morphogenesis, but instead had annotations and GO terms associated with behavioral or other physiological functions

3 transcripts that were DE in both transcriptome and proteom datasests ahd the same trend of expression
	
	3 proteins warrant further investigation


---

Accumulating evidence suggests that flatwing’s rapid response to selection on several Hawaiian islands may be linked to the expression of other traits, including plasticity in female responsiveness to acoustic signals (Bailey et al., 2008, Bailey & Zuk 2008, Tinghitella et al., 2009), male reproductive tactics and morphology (Bailey et al., 2010), immunity (Bailey et al., 2011), locomotion (Balenger & Zuk 2015), and cuticular hydrocarbon profiles (Simmons et al., 2014). 













		











	