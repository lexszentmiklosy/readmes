#Git


git add -A 
Add all files to commit, including removing deleted files


git commit -m "initial commit"
commit with message

git push
push code to bitbucket


git pull


git pull origin master 
???

git checkout <file> 
to remove a single from new commit

git checkout -f
remove all files from new commit



git remote add {name} {Public Clone URL}
git pull {name} master
git push


git fetch https://bitbucket.org/dmgdirectv/template_static-website-generator.git
git checkout FETCH_HEAD -- Gruntfile.js package.json

#Vocabulary:
Origin: Remote Repo
Master: Main Branch


#Branching:
Make New Branch:
	
	git branch $BranchName

Switch to Branch:
	
	git checkout $BranchName

Make a new Branch AND Switch to it
	
	git checkout -b $BranchName

Delete Branch:

	git branch -D $BranchName


#Remotes

Show all remote Repositories
	
	git remote
	
Show all remote repositories with URLS
WHY IS THERE A FETCH AND PULL?
	
	git remote -v
	
	
Rename a remote repository

	git remote rename $oldName $newName
	
Remove a remote repository

	git remote rm $repoName
	
	
	


#Pushing

Push to remote
	
	git push $remoteName $branchName (Is this Remote Branch or Local branch)
	
	
#Pulling

Pull from remote
	
	git pull $remoteName $branchName (Is this Remote Branch or Local branch)
	
	

# Pull Requests

Work in your own branch, not master
	
	git checkout $MyBranch
	

Commit changes 

	git add -A
	git commit -m "Commiting changes to $MyBranch"
	

Pull Master(remote) branch into your branch to ensure your code is up to date before placing a pull request

	git pull origin master
	
Fix all merge Issues

	git status
	git add -A
	git commit -m "Merged Master Branch into $MyBranch"
	
	
Push to your remote branch.

	git push
	
	
In BitBucket goto pull requests and Create Pull Request from $MyBranch -> Master

Pull requests are from the perspective on the admin. You are REQUESTING that the ADMIN PULL $YouBranch into Master


Merge Issues 
	
	<<<<< HEAD
		Code from your local commit
	======
		Code from remote branch 
	>>>> c9a86773bb1525f7617145 (Commit #)
	
	







