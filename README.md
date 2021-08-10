# GIT-Essentials

## Log Commits
```python
# 1. Filter the commit log

git log 	# displays list of commits
	
git log --oneline	 # displays a list of commits in a line

git log -3	# displays the last 3 commits

git log --since=2019-04-13  # displays commits since date

git log --until="3 days ago" # display commits until 

git log --after="2 weeks" --before="3 days"

git log --author="Kevin"  # displays Kevin commits
			
git log --author="Sally"	# displays Sally commits

git log --grep='Initial commit'				

git log b447401938..HEAD					

git log explore.html	# display commits of a particular file

# 2. Format the commit log

git log -p 	 # patch the change between

git log --stat 	# shows statistics of what has changed

# Log format
git log --format=short 		# format the commit log
git log --format=medium
git log --format=oneline

git log --oneline 	# shortens the SHA

git log --graph			

git log --graph --all --oneline --decorate
```

## Setting up local repository on remote

```python

cd project_name 

cat .git/config 	# check for remote URL
  '''
  [core]
        repositoryformatversion = 0
        filemode = true
        bare = false
        logallrefupdates = true
        ignorecase = true
        precomposeunicode = true
  [remote "origin"]
        url = REPLACE_WITH_YOUR_URL
        fetch = +refs/heads/*:refs/remotes/origin/*
  '''

# Change remote url with username url
git remote
  origin

# Remove origin
git remote rm origin

# Add remote url
git remote add origin https://github.com/username/demo_repo.git

# Add feature_branch to remote url
git push origin master

# First version

  # To create & track new feature branches
    
    git branch
      * master

    git checkout -b feature_branch_1									
    git push -u origin feature_branch_1		# add & track feature_branch_1 to remote 

    git branch
      * feature_branch_1
      master

    git checkout master
    
    git branch
      * master
      feature_branch_1

    git checkout -b feature_branch_2																	
    git push -u origin feature_branch_2		# add & track feature_branch_2 to remote

    git branch
      feature_branch_1
      * feature_branch_2
      master

    cat .git/config	 # check if the new feauture branches are tracked
      '''
      [core]
            repositoryformatversion = 0
            filemode = true
            bare = false
            logallrefupdates = true
            ignorecase = true
            precomposeunicode = true
      [remote "origin"]
            url = https://github.com/username/demo_repo.git
            fetch = +refs/heads/*:refs/remotes/origin/*
      [branch "master"]
            remote = origin
            merge = refs/heads/master
      [branch "feature_branch_1"]
            remote = origin
            merge = refs/heads/feature_branch_1
      [branch "feature_branch_2"]
            remote = origin
            merge = refs/heads/feature_branch_2
      '''

    # To untrack remote branches
      git branch --unset-upstream feature_branch_1
      git branch --unset-upstream feature_branch_2

# Second version

  # To create & track new feature branches
	  git branch
      * master

	git branch -u origin/master master
	git branch -u origin/feature_branch_1 feature_branch_1	
	git branch -u origin/feature_branch_2 feature_branch_2	
	git push origin master
	git push origin feature_branch_1
	git push origin feature_branch_2
	
  cat .git/config		# check if the new feauture branches are tracked

  # To untrack remote branches
    git branch --unset-upstream feature_branch_1
    git branch --unset-upstream feature_branch_2


```

## Check Remote Branches

```python
git branch -r # show remote branches
  origin/master
  
git branch -a # show all branches

ls -la .git/refs/remotes

cat .git/refs/origin/remotes/origin

cat .git/refs/origin/remotes/origin/remote

```

## Branching
```python

# Create new_feature branch and stay in master branch

cat .git/HEAD 	# displays Git reference
  ref: refs/heads/master

git branch
  * master

git branch new_feature 	# create new_feature branch

git branch
  * master
  new_feature

cat .git/refs/heads/master

git checkout new_feature

git branch
  master
  * new_feature

git push -u origin new_feature 	# create remote tracking new_feature 

# Create & switch to new_feature branch

cat .git/HEAD 	# displays Git reference
  ref: refs/heads/master

git checkout -b new_feature 	

git branch
  master
  * new_feature

git push -u origin new_feature	# create remote tracking new_feature 

```

## Stage & Unstage files
```python

git branch
  * master

git checkout -b new_feature

git branch
  master
  * new_feature

# Make changes to a file (e.g. mission.html)

# stage file
git add mission.html

# unstage file 
git reset HEAD mission.html

```

## Track Changes
```python

git branch
  * master
  new_feature

git checkout new_feature

git branch
  master
  * new_feature

# Make changes to a file (e.g. mission.html)

git status

git commit -am "Change title in mission page"

git status

# Message: "Nothing to commit"

```

## Stash Changes
```python

git branch
  * master
  reset_branch
  seo_title
  shorten_title
  text_edits

git checkout shorten_title
  master
  reset_branch
  seo_title
  * shorten_title
  text_edits

# Make changes to a file (e.g. mission.html) 

git status
	# modified: mission.html

git checkout master

# Message: "Error, please commit your changes or stash them before you switch branches"

git stash save "changed mission page title"

git status

# Message: "Nothing to commit, working tree"


# View stashed changes
git stash list
	# "changed mission page title"

git stash show stash@{id}


# Retrieve stashed changes
git stash list 

git stash apply


# Delete stashed changes
git stash list	# list stashes

git stash save "Delete me" # saves new stash

git stash list	# list stashes

git stash drop stash@{id}

git stash clean # clean everything

git stash pop	# removes the stash

```

## Remove Last Commit

```python

git reset HEAD^ # remove commit locally

git push origin +HEAD # force-push the new HEAD commit

```

## Rename Branches
```python

git branch
  * master
  new_feature
  shorten_title

# Rename new_feature -> seo_title
git diff master..new_feature

git checkout new_feature

git branch -m seo_title

git branch
  master
  * seo_title
  shorten_title 

```

## Compare Branches
```python

git branch
  * master
  new_feature
  shorten_title

# Compare master with new_feature
git diff master..new_feature

# Compare master with shorten_title
git diff master..shorten_title

# Compare new_feature with shorten_title
git diff new_feature..shorten_title

# Compare and show color changes
git diff --color-words new_feature..shorten_title

```

## Merge Branches
```python

git branch
  master
  new_feature
  * reset_branch
  seo_title

git checkout master

# Bring changes from seo_title into master

git diff master..seo_title

git merge seo_title

git diff master..seo_title

git branch --merged # check merged branches
git branch --no-merged # check not merged branches

```

## Merge Conflicts
```python


# Solution:
#  * abort merge
#  * resolve the conflicts manually
#  * use a merge tool

# To resolve the conflicts manually
git branch
  * master
  reset_branch
  seo_title
  shorten_title

# Resolve conflicts for text_edits with master branch
git checkout -b text_edits

git branch
  master
  reset_branch
  seo_title
  shorten_title
  * text_edits

# Make change in one file (e.g. mission.html)
git commit -am "Text edits to mission page"

git log --oneline -5
git log text_edits --oneline -5

git checkout master

# Make a change in master to the same mission.html page
git commit -am "Replaces straight quotes with curly quotes"

git log text_edits --oneline -5

git branch
  * master
  reset_branch
  seo_title
  shorten_title
  text_edits

git merge text_edits
# Message: Error, merge conflict in mission.html 

git status

# Solutions:
	
	# 1) abort the operation
		  
      git merge --abort

	# 2) merge conflict : fix commits -> rename Git tags and keep the right text
	
      git diff --color-words master..text_edits

      git add mission.html

      git status

      git commit 

      git merge text_edits

      git log --graph --all --oneline --decorate


# Strategies to reduce conflicts:
#  * keep lines short
#  * keep commits small & focused
#  * merge often
#  * track changes to master

```

