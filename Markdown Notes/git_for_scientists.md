##Git for Scientists

### Chapter 5

Helps with project organization especially when working collaboratively - managing code and data.

Helpful if you want to rewind to a past snapshot of your project's state and restore files.

Have an entire history of all your project's changes and can pinpoint when your results change

Git Setup:

	$ git config --global user.name "Sewall Wright"
	$ git config --global user.email "swright@adaptivelandscape.org"
	
Creating Repositories:

1) by initializing one from an exisiting directory 

	$ git init
	Initialized empty Git repository

git init creates a hidden directory called .git/ in your project directory
	
2) cloning a repository that exists elsewhere	

	$ git clone git://github.com/lh3/seqtk.git
	clones seqtk to your local directory

You need to tell git what files to track with git add subcommand

Use git status to see the current state of your project respository - what has changed and what's ready to be included in the next commit.

	$ git add README data/README
	
Tracked files mean that Git knows about it and a staged file is tracked and the latest changes are included in the next commit. 

You need to add them using git add to stage the file	
	
Seeing File Differences:

git diff - will show you the difference between the files in your working directory and what's been staged

	git diff --staged
	
	use this if we want to compare what's been staged to our last commit
	
Visualize our chain of commits:

We can use git log 

	$ git log
	commit ...
	Author: ...
	Date: ...
	
Moving and Removing Files:


git mv to move/rename files and git rm to remove files

	$ git mv README README.md
	$ git mv data/README data/README.md
	

Telling Git What to Ignore:	

Ex. Want to ignore all FASTQ files

	data/seq/*.fastq
	
	$ git status
	$ On branch master
	$ Untracked files: ...
		
		.gitignore
		
Best way is to add and commit .gitignore file, saves collaborators from seeing a listing of untracked files

	$ git add .gitignore
	$ git commit -m "added .gitignore"
	
What should we tell git to ignore?

- Large files

- Intermediate files

- Text editor temporary files

- Temporary code files	


Undoing a Stage: git reset

If you accidentally stage a messy file for commit with git add, you can unstage it with git reset

	$ git reset HEAD README.md
	
	HEAD is an alias or pointer to the last commit on the current branch
	
	
####Collaborating with Git

1. You create a shared central repository on a server that both you and your collaborator have access to 

2. You push your project's initial commits to this repository

3. Your collaborator then retrieves your initial work by cloning this central repository

4. Then, your collaborator makes her changes to the project, commits them to her local repository, and then pushes these commits to the central repository

5. You then pull in the commits your collaborator pushed to the central repository. The commit history of your project will be a mix of both you andn your collaborator's commits.

Helpful to frequently push and pull commits to the central repository

Authenticating with Git remotes

GitHub uses SSH keys to authenticate you - prevents you from having to enter a password each time you push or pull from your remote repository 

Enter your public SSH key by using cat ~/.ssh/id_rsa.pub to view it, copying it to your clipboard and pasting into GitHub's form

Connecting with Git remotes:

To configure our local repository to use the GitHub respository:

	$ git remote add origin git@github.com:username/zmays-snps.git
	
	$ git remote -v
	origin 	git@github.com:username/zmays-snps.git (fetch)
	origin  git@github.com:username/zmays-snps.git (push)
	
If you ever need to delete an unused remote repository, you can with git remote rm <repository-name>

Push commits to a remote repository with git push

	$ git push origin master
	
Pulling commits from a remote repository with git pull. Make sure to push changes first before pulling.

	$ git pull origin master
	

Merge Conflicts

1. Use git status to find the conflicting file

2. Open and edit thos files manually to a version that fixes the conflict

3. Use git add to tell Git that you've resolved the conflict in a particular file

4. Once all conflicts are resolved, use git status to check that all changes are staged. Then commit the resolved versions of the conflicting file. Push this merge commit, let collaborators know that you've resolved a conflict and continue working.

####Working with Branches

- Branches allow you to experiment in your project without the risk of adversely affecting the main branch, master.  	


- If you're developing software, branches allow you to develop new features or bug fixes without affecting the working production version

- Branches simplify working collaboratively on repositories. Each collaborator can work on their own separate branches which prevents disrupting the master branch for other collaborators. When a collaborators changes are ready to be shared, they can be merged into the master branch

Example: Create a new branch called readme-changes

Want to make some edits to README but we're not sure these changes are ready to be incorporated into the main branch

	$ git branch readme-changes
	$ git branch
	* master
	  readme-changes
	  
	Asterik next to master means that this is the branch we're currently on
	
To switch to the readme-changes branch, use git checkout reade-changes:

	$ git checkout readme-changes
	Switched to branch 'readme-changes'
	
	$ git branch
	  master
	 * readme-changes
	 
Now we can edit the README.md section and if we commit these changes, our commit is added to the readme-changes branch. We can verify this by switching back to the master branch and seeing that this commit doesn't exist

Merging Branches

First, use git checkout to switch to thre branch we want to merge the other branch into. Then, use git merge <otherbranch> to merge the other branch into the current branch

	$ git merge readme-changes
	 
		  



	
	
	



	





			
		
		
	
			
	
	