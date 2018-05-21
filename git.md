# Git

upstream (remote original project) <-> origin (remote fork of project) <-> local (fork)

## Online Guides
* [Simple git overview](http://rogerdudler.github.io/git-guide/)
* [git workflow](https://gist.github.com/Chaser324/ce0505fbed06b947d962)
* [Syncing a fork](https://help.github.com/articles/syncing-a-fork/)

## clone
```
git clone <url-to-project>
# keep clone in sync
git pull origin master

git clone <url-to-project> --branch <branch>
# keep clone in sync
git pull origin <branch> --recurse-submodules
```
## setup fork
```
# promote origin to upstream
git remote rename origin upstream
# add new fork as orign
git add remote origin <url-to-fork>
# view remote setup
git remote -v
```
## branch
```
# create a branch
git checkout -b feature/x
# delete a branch
git branch -d feature/x
```
## workflow
```
git checkout <branch>
git add <filename>
git commit -m "comment"
git push origin <branch>

# keep branch in sync...
git fetch upstream
git checkout <branch>
# ... by merge
git merge upstream/master
# ... OR by rebase
# keep branch in sync with master by rebase (rewind and reapply)
git rebase upstream/master

# update submodules
git submodule update --recursive
```
## Merge Conflict Markers
Git marks up a file with merge conflicts but it can be different based on if you did a pull (fetch/merge) or a rebase
```
# Pull (fetch/merge)
<<<<<<< HEAD
code from the branch you are merging into (your changes)
=======
code from the commit you are merging in (the remote changes)
>>>>>>>

# Rebase
<<<<<<< HEAD
code from the branch you are re-basing into (the remote changes)
=======
code from the branch you are replaying changes into (your changes)
>>>>>>>
```
## Tracking
View what a local branch may be tracking (should show up between [])
```
$ git branch -vv
* master 30092fc [upstream/master] notes from last checkin
  newdev 30092fc notes from last checkin
```
Can change a branch tracking:
```
$ git branch --set-upstream-to upstream/master master
Branch master set up to track remote branch master from upstream.
```
## Example script to keep multiple projects in sync under one top-level folder
```
echo Updating Clones...
clones=( project1 project2 project3 )
for i in "${clones[@]}"
do
	cd $i
	git pull origin master --recurse-submodules
	cd -
done

echo Updating Forks...
forks=( project4 project 5 )
for i in "${forks[@]}"
do
	cd $i
	git fetch upstream
	git checkout master
	git merge upstream/master
	git submodule update --recursive
	cd -
done
```
