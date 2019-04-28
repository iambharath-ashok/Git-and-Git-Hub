# Git Interview Questions

###	What is the difference between Git and SVN?

-	Git vs SVN

	|-------------------------------------------------------------------|--------------------------------------------------------------	|
	|				Git												    |			     			SVN                              	|
	|-------------------------------------------------------------------|--------------------------------------------------------------	|
	| 1. Git is a Decentralized Version Control tool	                    |  1. SVN is a  Centralized Version Control tool             	|
	| 2. It belongs to the 3rd generation of Version Control tools	    |  2. It belongs to the 2nd generation of Version Control tools |
	| 3. Clients can clone entire repositories on their local systems	|  3. Version history is stored on a server-side repository     |
	| 4. Commits are possible even if offline	                        |  4. Only online commits are allowed                           |
	| 5. Push/pull operations are faster	                                |  5. Push/pull operations are slower                           |
	| 6. Works are shared automatically by commit	                    |  6. Nothing is shared automatically                           |

### In Git how do you revert a commit that has already been pushed and made public?

-	There can be two answers to this question and make sure that you include both because any of the below options can be used depending on the situation:

	-	Remove or fix the bad file in a new commit and push it to the remote repository. This is the most natural way to fix an error. Once you have made necessary changes to the file, commit it to the remote repository for that I will use
	git commit -m “commit message” 

	-	Create a new commit that undoes all changes that were made in the bad commit.to do this I will use a command
	
	git revert <name of bad commit>


###	What is Git stash?

-	According to me you should first explain the need for Git stash.

-	Often, when you’ve been working on part of your project, things are in a messy state and you want to switch branches for sometime to work on something else. The problem is, you don’t want to do a commit of half-done work just so you can get back to this point later. The answer to this issue is Git stash.

-	Now explain what is Git stash. 

-	Stashing takes your working directory that is, your modified tracked files and staged changes and saves it on a stack of unfinished changes that you can reapply at any time.


###	What is Git stash drop?

-	Begin this answer by saying for what purpose we use Git ‘stash drop’.

-	Git ‘stash drop’ command is used to remove the stashed item. It will remove the last added stash item by default, and it can also remove a specific item if you include it as an argument.

-	Now give an example.

-	If you want to remove a particular stash item from the list of stashed items you can use the below commands:

		git stash list
		git stash apply stash@{0}

		git stash list: It will display the list of stashed items like:
		stash@{0}: WIP on master: 049d078 added the index file
		stash@{1}: WIP on master: c264051 Revert “added file_size”
		stash@{2}: WIP on master: 21d80a5 added number to log

-	If you want to remove an item named stash@{0} use command git stash drop stash@{0}.

		git stash drop stash@{0}



### How do you find a list of files that has changed in a particular commit?


-	For this answer instead of just telling the command, explain what exactly this command will do.

-	To get a list files that has changed in a particular commit use the below command:

		git diff-tree -r {hash}

-	Given the commit hash, this will list all the files that were changed or added in that commit. The -r flag makes the command list individual files, rather than collapsing them into root directory names only.

-	You can also include the below mentioned point, although it is totally optional but will help in impressing the interviewer.

-	The output will also include some extra information, which can be easily suppressed by including two flags:

-	git diff-tree –no-commit-id –name-only -r {hash}

-	Here –no-commit-id will suppress the commit hashes from appearing in the output, and –name-only will only print the file names, instead of their paths.


### 	What is the function of ‘git config’?

-	Git uses your username to associate commits with an identity. The git config command can be used to change your Git configuration, including your username.

-	Now explain with an example.

-	Suppose you want to give a username and email id to associate commit with an identity so that you can know who has made a particular commit. For that I will use:

		git config –global user.name “Your Name”: This command will add username.
		git config –global user.email “Your E-mail Address”: This command will add email id.


###	What does commit object contains?

-	Commit object contains the following components, you should mention all the three points present below:

	-	A set of files, representing the state of a project at a given point of time
	-	Reference to parent commit objects
	-	An SHAI name, a 40 character string that uniquely identifies the commit object.

###	How can you create a repository in Git?

-	This is probably the most frequently asked questions and answer to this is really simple.

-	To create a repository, create a directory for the project if it does not exist, then run command “git init”. By running this command 	.git directory will be created in the project directory.

###	How do you squash last N commits into a single commit?


-	There are two options to squash last N commits into a single commit 

	
	-	If you want to write the new commit message from scratch use the following command
			git reset –soft HEAD~N &&
			git commit
		
	-	If you want to start editing the new commit message with a concatenation of the existing commit messages then you need to extract those messages and pass them to Git commit for that I will use

			git reset –soft HEAD~N &&
			git commit –edit -m”$(git log –format=%B –reverse .HEAD@{N})”




###	What is Git bisect? How can you use it to determine the source of a (regression) bug?

-	Git bisect is used to find the commit that introduced a bug by using binary search. Command for Git bisect is
		
		git bisect <subcommand> <options>

-	This command uses a binary search algorithm to find which commit in your project’s history introduced a bug. 
-	You use it by first telling it a “bad” commit that is known to contain the bug, and a “good” commit that is known to be before the bug was introduced.
- 	Then Git bisect picks a commit between those two endpoints and asks you whether the selected commit is “good” or “bad”. 
-	It continues narrowing down the range until it finds the exact commit that introduced the change.	


###	Describe branching strategies you have used?

-	Release branching
-	Feature branching
-	Task branching

###	How will you know in Git if a branch has already been merged into master?

-	To know if a branch has been merged into master or not you can use the below commands:

		git branch –merged 
		
		-	It lists the branches that have been merged into the current branch.
		
		git branch –no-merged 
		
		-	It lists the branches that have not been merged.


###	What is Git rebase and how can it be used to resolve conflicts in a feature branch before merge?

-	git rebase is a command which will merge another branch into the branch where we are currently working
-	And move all of the local commits that are ahead of the rebased branch to the top of the history on that branch
-	If a feature branch was created from the master, and since then the master branch has received new commits, Git rebase can be used to move the feature branch to the tip of master
-	The command effectively will replay the changes made in the feature branch at the tip of master, allowing conflicts to be resolved in the process
-	When done with care, this will allow the feature branch to be merged into master with relative ease and sometimes as a simple fast-forward operation

###	What is SubGit?

-	SubGit is a tool for SVN to Git migration
-	Subgit’ is a tool for a smooth, stress-free SVN to Git migration. 
-	Subgit is a solution for a company -wide migration from SVN to Git that is:

	-	a) It is much better than git-svn
	-	b) No requirement to change the infrastructure that is already placed
	-	c) Allows to use all git and all sub-version features	
	-	d) Provides genuine stress –free migration experience.

###	Why GIT better than Subversion?

-	Multiple developers can checkout, and upload changes and each change can then be attributed to a specific developer.
-	GIT is an open source version control system; it will allow you to run ‘versions’ of a project, which show the changes that were made to the code overtime also it allows you keep the backtrack if necessary and undo those changes.


###	What is ‘bare repository’ in GIT?

-	To co-ordinate with the distributed development and developers team, 
-	Especially when you are working on a project from multiple computers ‘Bare Repository’ is used. 
-	A bare repository comprises of a version history of your code.


###	Name a few Git repository hosting services

-	Bit Bucket
-	Git Hub
-	Git Lab


###	Why is it advisable to create an additional commit rather than amending an existing commit?

-	There are couple of reason:
	-	1.
		-	The amend operation will destroy the state that was previously saved in a commit
		-	If it’s just the commit message being changed then that’s not an issue
		-	But if the contents are being amended then chances of eliminating something important remains more

	2.	using “git commit -amend” can cause a small commit to grow and acquire unrelated changes	

###	How can you fix a broken commit?

-	To fix any broken commit, we will use the command “git commit —amend”.
-	By running this command, we can fix the broken commit message in the editor.

###	Explain what is commit message?

-	Commit message is a feature of git which appears when you commit a change. 
-	Git provides you a text editor where you can enter the modifications made in commits.

### What does ‘hooks’ consist of in git?

-	This directory consists of Shell scripts which are activated after running the corresponding Git commands. 
-	For example, git will try to execute the post-commit script after you run a commit.

###	What is git Is-tree?

-	‘git Is-tree’ represents a tree object including the mode and the name of each item and the SHA-1 value of the blob or the tree


### What is the function of ‘git reset’?

-	The function of ‘Git Reset’ is to reset your index as well as the working directory to the state of your last commit.


###	What is ‘git add’ is used for?

-	‘git add’ adds file changes in your existing directory to your index.

###	What is the use of ‘git log’?

-	To find specific commits in your project history- by author, date, content or history ‘git log’ is used

### What is the function of ‘git stash apply’?

-	When you want to continue working where you have left your work, 
-	‘git stash apply’ command is used to bring back the saved changes onto the working directory.

	git stash apply stash@{0}

###	  What is the function of ‘git rm’?

-	To remove the file from the staging area and also off your disk ‘git rm’ is used
	
		git rm <Filename>

###	What is the function of ‘git checkout’ in git

-	A ‘git checkout’ command is used to update directories or specific files in your working tree with those from another branch 
	-	without merging it in the whole branch	

###	What is the function of ‘git diff ’ in git?

-	git diff ’ shows the changes between commits, commit and working tree etc.

###	What is ‘git status’ is used for?

-	As ‘Git Status’ shows you the difference between the working directory and the index,
-	it is helpful in understanding a git more comprehensively

###	What is the difference between the ‘git diff ’and ‘git status’?

-	‘git diff’ is similar to ‘git status’, 
-	But it shows the differences between various commits 
-	And also between the working directory and index


###	What is the difference between ‘git remote’ and ‘git clone’?

-	‘git remote add’  just creates an entry in your git config that specifies a name for a particular URL. 
-	While, ‘git clone’ creates a new git repository by copying and existing one located at the URI.


###	What is another option for merging in git?

-	“Rebasing” is an alternative to merging in git.


### What is the syntax for “Rebasing” in Git

-	The syntax used for rebase is “git rebase [new-commit] “

### To delete a branch what is the command that is used?

-	Once your development branch is merged into the main branch, you don’t need

### What is a ‘conflict’ in git?

-	A ‘conflict’ arises when the commit that has to be merged has some change in one place, 
-	And the current commit also has a change at the same place.
-	 Git will not be able to predict which change should take precedence.

###	How can you bring a new feature in the main branch?

-	To bring a new feature in the main branch, you can use a command “git merge” or “git pull command”.


###	What is ‘head’ in git and how many heads can be created in a repository?

-	A ‘head’ is simply a reference to a commit object.
-	In every repository, there is a default head referred as “Master”.
-	A repository can contain any number of heads.

### What is the common branching pattern in GIT?

-	The common way of creating branch in GIT is to maintain one as “Main“

-	branch and create another branch to implement new features.
- 	This pattern is particularly useful when there are multiple developers working on a single project.


### What is Git fork? What is difference between fork, branch and clone?

-	A fork is a remote, server-side copy of a repository, distinct from the original. A fork isn't a Git concept really, it's more a political/social idea.

-	A clone is not a fork; a clone is a local copy of some remote repository.
	- 	When you clone, you are actually copying the entire source repository, including all the history and branches.

-	A branch is a mechanism to handle the changes within a single repository in order to eventually merge them with the rest of code.
-	A branch is something that is within a repository. Conceptually, it represents a thread of development

###  What's the difference between a "pull request" and a "branch"

-	A branch is just a separate version of the code.

-	A pull request is when someone take the repository, makes their own branch, does some changes, then tries to merge that branch in (put their changes in the other person's code repository).


###	What is the difference between "git pull" and "git fetch"

### Explain the advantages of Forking Workflow
### Tell me the difference between HEAD, working tree and index, in Git?	

###	Could you explain the Gitflow workflow?

-	Gitflow workflow employs two parallel long-running branches to record the history of the project, master and develop:

	-	Master: is always ready to be released on LIVE, with everything fully tested and approved (production-ready).
	
	-	Hotfix: Maintenance or “hotfix” branches are used to quickly patch production releases. Hotfix branches are a lot like release branches and feature branches except they're based on master instead of develop.
	
	-	Develop:  is the branch to which all feature branches are merged and where all tests are performed. Only when everything’s been thoroughly checked and fixed it can be merged to the master.
	
	-	Feature: Each new feature should reside in its own branch, which can be pushed to the develop branch as their parent one.


###	How to remove a file from git without removing it from your file system?

-	If you are not careful during a git add, you may end up adding files that you didn’t want to commit. 
-	However, git rm will remove it from both your staging area (index), as well as your file system (working tree),
-   which may not be what you want.

	Instead use git reset:

		git reset filename          # or
		echo filename >> .gitingore # add it to .gitignore to avoid re-adding it


### When do you use "git rebase" instead of "git merge"?

-	Both of these commands are designed to integrate changes from one branch into another branch - they just do it in very different ways
-	When to use:

	-	If you have any doubt, use merge.
	-	The choice for rebase or merge based on what you want your history to look like.