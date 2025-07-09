## For uploading a directory on git:
```bash
	git init
	git add .
	git commit -m "initial commit"
	git remote add origin https://github.com/siddhant2155/test
	git pull origin master      (press :wq)
	git push origin master

	(if doing for 2nd time then don't add origin)
	git add .
	git commit -m "second commit"
	git pull origin master      (press :wq)
	git push origin master
```	
	
```bash
git status : to check the status if new file is added or not.
git log : to check the logs.
```

## Git Alias
```bash
	git config --global alias.br branch
	git config --global --unset alias.br # to unset alias
```

## Git Remote
```bash
git remote 		<==>		git remote show
git remote -v
git remote add [options] [remote_name] [repo_url]
git remote rm/remove [remote_name]
git remote rename <old_name> <new_name>
git remote show [remote_name]
```

## Git Revert
- It is consdered as an `undo` type command.
- Instead of removing the commit from the project history, it figurres out how to invert the changes introduced by the commit and appends a new commit with the resulting inverse content.
```bash
git revert [options] HEAD
git revert -e | --edit <commit_id> 	(Default option)
git revert --no-edit <commit_id>
git revert -n | --no-commit <HEAD~count_of_commit>
```

## [Git Reset](https://www.atlassian.com/git/tutorials/undoing-changes/git-reset)
```bash
git reset [option] <commit>
		--mixed
		--soft
		--hard
```		


## Git Add 
```
git add .
git add [file]
git add -A / --All
git add -u / --update
```

## Git Checkout and Branch
```bash
git checkout -b "branchName"
git checkout "switchingBranchName"
git branch
git branch [new_branch_name]
git branch [new_branch_name] <commit id>
git brnach [new_branch_name] remote_branch_name to add remote brnach in local repo
git branch -d [branch_name]			soft delete
git branch -D [branch_name]			forcefully delete
git branch -n [new_name]			rename current branch
git brnach -m [old_branch_name] [new_name]	rename any brnach
git branch -a					list all remote branch
git push [remote_name] --delete [branch_name] 	to delete branch from repo.
```

## Git commit 
```
git commit -m ""
git commit -am ""
	commit all tracked file without adding them in staging area.
git commit --amend 
	alter the latest commit
git commit --allow-empty -m ""
	add a empty commit
```

## Git Merge
```
git merge <branch_name>
git merge --no-ff <branch_name>
	Merge Branch will not be fast-forwarded [use diff merge strategy]
git merge --no-commit <branch_name>
git merge --no-ff --no-commit <branch_name>
```

## .gitignore
```
vim .gitignore
```
If you already have a file checked in, and you want to ignore it, Git will not ignore the file if you add a rule later. In those cases, you must untrack the file first, by running the following command in your terminal:

`$ git rm --cached FILENAME`
https://help.github.com/en/articles/ignoring-files

`$ git config --global core.excludesfile ~/.gitignore_global`

## Git Stage
```
git stage [file]
```
It is a synonym of `git add`

## Git log
```
git log
git log -p		<==> 		git show
git log --stat
git log --oneline --graph
git log <branch_name> [options]
git log --branch=*
```

## Git diff
```
git diff --staged
git diff
git diff file
git diff [first-branch]...[second-branch]
```

## Git stash
```
git stash
git stash --all		[also include untracked file]
git stash save [msg]
git stash push
git stash push --all		[also include untracked file]
	use to save uncommitted change (both staged & unstaged)
git stash -p
	stash chunck of code
git stash show
	Show the changes recorded in the stash as a diff between the stashed state and
       its original parent
git stash pop
git stash apply [stash name/id]
	remove stash
git stash list
git stash drop [stash name/id]
git stash clear
```

## Git Tag
```
git tag <tag_name>
git tag <tag_name> -m "msg"
git tag -a <tag_name>				create annotated tag
git tag
git show <tag_name>

git push <remote_name>	[tag_name]
git push <remote_name> --tags

git tag -d [tag_name]
git tag --delete [tag_name]

git push <remote_name> -d [tag_name]
git push <remote_name> --delete [tag_name]
git push <remote_name> :[tag_name]
```

---
## Remove all global users:
```	
	git config --global --unset-all user.name
	git config --global --unset-all user.email
 ```
	
## List all global users:
```	git config --global --list```
	
## Setting your git username for every repository on your computer:

### Set a git username:
```
git config --global user.name "Mona Lisa"
```

### Confirm that you have set the git username correctly:
```	
git config --global user.name
```
    
## Setting your git username for a single repository:

   #### Change the current working directory to the local repository where you want to configure the name that is associated with your Git commits.

   ### Set a git username:
```
git config user.name "Mona Lisa"
```

  ###  Confirm that you have set the git username correctly:
```bash
git config user.name
Mona Lisa
```

### SSH (Secure Shell)
```
	https://help.github.com/en/articles/connecting-to-github-with-ssh
```
  ### Git Alias
```
	git config --global alias.br branch
	git br
```

---

# Fix detached HEAD
` git checkout origin/master `


## BitBucket :
```	git pull origin master --allow-unrelated-histories```

---
## Install git on Linux :
```
	sudo apt-get update
	sudo apt-get install git
	git config --global user.name "Mona Lisa"
	git config --global user.email "mona@example.com"
```


## LFS
Git *Large File Storage*
[https://git-lfs.com/](https://git-lfs.com/)
