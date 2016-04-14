These commands will update command line Java and install command line IGV. You need to do this on your local machine, not your instance.

	$ brew install Caskroom/cask/java
	$ brew install igv
	

Let's also update Java for our web browser (Firefox). Go here:

	http://www.oracle.com/technetwork/java/javase/downloads/index.html
	
Make sure you pick Java for the Mac.

To download IGV and use it with a GUI, go here:

	http://www.broadinstitute.org/software/igv/home
	
You will have to register to download it, but it's free.

Connect to your instance to do the exercises in Chapter 11. Before you can use samtools, you will need to use the following command:

	$ module load samtools/1.1
	
Recall that you also had to do this to run sequence trimming programs Scythe and Sickle, so if you've got a program that doesn't seem to be running on your instance but you see that it's installed, try the module load command and specify the program and it's version number.

**For examples that deal with the human_g1k_v37.fasta file.** We don't have space on the instance to unzip the file and I couldn't get it to work even when I resized the instance to a much larger size. Therefore, to do these examples, you will need to install Samtools on your local machine. We installed Homebrew a number of weeks ago, so you should be able to install Samtools with:

	$ brew install samtools

The file is from the 1000 Genomes Project and can be obtained using wget:

	$ wget ftp://ftp.1000genomes.ebi.ac.uk/vol1/ftp/technical/reference/human_g1k_v37.fasta.gz

See the README.md file for this chapter.

To do the IGV section, you will need to use scp to copy your NA12891_CEU_sample.bam and NA12891_CEU_sample.bam.bai files from your instance to your local machine.

**Make sure you take notes on SAM/BAM and VCF formats from this chapter.**

###If you have time and have completed all other variant calling activities on Moodle, you can try PySam if you like.

####PySam is a set of tools developed using the Python programming language to work with alignment data.

You can install PySam on your instance using the command:

	$ sudo pip install pysam
	
Sudo stands for "super user do!" and is something you can use to get around permissions that you may not have unless you are a user with administrative access. If you install Pysam on your local machine, you shouldn't need the "sudo" part of the command.

To access Python in your instance, write:

	$ python

You will get the Python command prompt ">>>". Then you will be able to do Python examples or execute Python scripts. To exit Python, hit _ctrl-D_.