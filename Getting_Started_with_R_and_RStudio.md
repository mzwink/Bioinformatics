##Getting Started with R and R Studio

###Download and Install R

Go to: 
	
	https://www.r-project.org/
	
Then find the CRAN mirror closest to you (there is one at the Hutch) and download the installation package (choose this one: http://cran.fhcrc.org/). Open it and follow the installation instructions.
	
###Download and Install R Studio

Go to:

	https://www.rstudio.com/
	
Once you have installed R Studio, you will want to add some useful packages. A popular graphics package is ggplot2. Let's install it so you can use it later on. To learn more about ggplot2, visit the homepage (http://ggplot2.org/).

In R Studio, type the install command for ggplot2:

	install.packages("ggplot2")
	
Once that's installed, let's install Bioconductor (http://www.bioconductor.org/), which is a bioinformatics package for R that might come in handy.

In R Studio:

	source("https://bioconductor.org/biocLite.R")
	biocLite()
	
When you are asked about updating, answer "a".

We will be using files from Bioinformatics Data Skills today. If you do not have the data files from Bioinformatics Data Skills on your local machine, open your Terminal window and use git to clone the repository of files from GitHub.

	$ git clone https://github.com/vsbuffalo/bds-files.git
	

	
