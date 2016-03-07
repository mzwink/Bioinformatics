## Analysis of Next-Generation Sequence Data

### Chapter 9 Pevsner Reading Notes


Next-generation sequencing (NGS):

	1. NGS enables determination of the DNA sequence of genomes across the entire tree of life
	
	2. Can compare an individual's sequence to a reference genome
	
	3. Compare the genetic differences within an individual across different cells types - somatic changes are important in cancer and can sequence genome from tumors and from nontumorous parts of the body of the same person
	
	4. NGS applied to RNA allows the measurement of RNA transcript levels
	
	5. Most life forms are single-celled organisms and uncultivatable as single species in a lab --> with metagenomics it is possible to apply NGS to environmental samples
	
Human genome = ~3.2 gigabases, much of it is repetative 

### DNA Sequencing Technologies

*Sanger Sequencing*

- most commonly used technique for sequencing DNA

- Obtain a template of interest (fragment of genomic DNA or cDNA), denature it to yield single-stranded  DNA, and add primer.

- Presence of DNA polymerase I and dNTP's--> synthesis of second strand 

- Separate reactions include ddNTPs which act as terminators

- Electrophoresis detects area within a DNA sequencing machine where a laser excites the fluorophores producing fluorescence emissions that correspond to base calls

- Can read as many as 300 bases in a set of reactions, current reads can approach 800 or more bases

- Sanger sequencing has error rates less than 1%

- Quality scores are given, want scores >20

### Next-Generation Sequencing

- Able to achieve reads of hundreds of base pairs

*Cyclic Reversible Termination: Illumina*

- Illumina can generate on terabase of DNA sequence data in a single run 

- Principle of cycle reversible termination:

	1. Genomic DNA is purified and then randomly fragmented.  Adapters are attached to both ends. 
	
	2. Single-stranded DNA fragments are covalently attached to the surface of flow cell channels
	
	3. The addition of DNA polymerase and unlabeled deoxynucleotides creates a solid-phase "bridge amplification"
	
	4. Double-stranded bridges formed, denatured and then amplified to generate dense clusters of template DNA
	
	5. Four lableled reversible terminators are added, only a single reversible terminator will be added to each template
	
	6. Laster excitation --> identity of the first base 
	
	7. For the second cycle, the reversible terminators are removed, all 4 labeled reversible terminators and polymerase are added again to the flow cell. Cycles are repeated
	
- Very fast and generates massive amount of sequence data

- Read lengths are typically 150 bases or longer which is appropriate for resequencing projects

- Illumina accounts for about 80% of all next-generation sequence data that are being generated


*Pyrosequencing*

- Roche Diagnostics Corporation

- Only one dNTP is added into the reaction at a time

- DNA is immobilized on beads that capture one single-stranded template that is amplified using the PCR

- The template is placed in small wells and one dNTP is added to the wells per cycle

- The reaction mixture contains the template DNA, a sequencing primer, four enzymes, APS and luciferin

- dNTP is added and is incorporated into the nascent strand until a different dNTP is required

- Each incorportaion leads to an equimolar amount of pyrophosphate (PPi) being generated --> ATP --> promotes luciferase-mediated conversion of luciferin to oxyluciferin with the generation of light

- The emitted light is detected with CCD camera and measured over time to indicate at which position a nucleotide was incorporated

- Advantages of pyrosequencing:

	1. Fast and cost is low
	
	2. One run can generate up to 600 megabases
	
	3. DNA molecules are amplified w/o need for bacterial cloning
	
	4. High accuracy
	
- Disadvantages:

	1. Sequencing reads are short making whole-genome assembly challenging
	
	2. Difficulty in sequencing homopolymers (a string of 10 identical nucleotides)
	
*Pacific Bioscience: Single-Molecule Sequencing with Long Read Lengths*

- Enables real-time sequencing of a DNA molecule using a DNA polymerase and 4 distinguishable labeled dNTPs

- Relies on a zero-mode waveguide nanophotonic structure: detection of single fluorophores 

- Read lengths can average 5000 base pairs and with high accuracy 	




















