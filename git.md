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
git pull origin <branch>
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

# keep fork in sync
git fetch upstream
git checkout master
git merge upstream/master

git checkout feature/x
git rebase master
```

## script to keep multiple projects in sync under one top-level folder
```
echo Updating Clones...
clones=( project1 project2 project3 )
for i in "${clones[@]}"
do
	cd $i
	git pull origin master
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
	cd -
done
```
