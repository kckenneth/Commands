3 critical steps in version control in git

1. git add <file name>
2. git commit -m <"message">
3. git push origin --all
 
### to make a local git repository
If you're doing your project locally and want to control version, you can do by installing git. After your local computer has git installed, you can make any directory as git repository. 
```
mkdir myproject       # creating myproject directory
cd myproject
git init              # initialize the git in `myproject` directory
git status            # checking the git status, you'd see you're on master branch
```

### To clone the repository from the github 
Or you can also clone the git repository locally. 
```
git clone https://github.com/kckenneth/Commands.git
<OR>
git clone https://github.com/kckenneth/Commands.git myCommands     # change the directory name to `myCommands`
```

### Fetch any updates from the git repo
 
```
git pull             # will pull master branch
git pull -all        # will pull all branches
git pull myBranch    # will pull myBranch
```
 
### to create a file 
```
cd Commands
mkdir testfolder
cd testfolder
nano test.txt
```

### to commit the changes in the folder created with a comment
```
git commit -m "added test file"
```

### check the difference
After you make the commit, and you make another modification on the file, you can check the difference between the committed file and a new file. A new file has not been committed yet. 
```
git status           # will tell you if there's any uncommitted file
git diff test.txt    # check the difference between the previously committed file and a newly modified file
```

### to create a branch "development" and checkout to the branch "development"
```
# to create the branch first
git branch development 
git checkout development

# to create and immediately checkout to the branch
git checkout -b development

# if the branch already exists
git checkout development  
```

### to checkout to master
```
git checkout master
```

### example of creating the branch and merging
```
$ git checkout -b topic #Create and checkout new branch
$ git commit -a -m "New Features" #Commit all the changes
$ git checkout master #Checkout to Master
$ git merge topic #Merge new branch "topic"
$ git branch -d topic #Delete new branch "topic"
```

### to know which remote repository you have in the directory
```
git remote -v

origin	https://github.com/kckenneth/GATECH.git (fetch)
origin	https://github.com/kckenneth/GATECH.git (push)
```

### to push the branch to remote repository
```
git push origin development        # development branch only
git push origin --all              # push all branches to origin repo
```

### revert to the last commit stage
```
git log                           # to get the last commit id, copy the id
git branch -D development         # to delete the branch that you don't want
git push origin :development      # to push to the remote `origin` to make changes as here in local branch
git reset --hard <commit id>      # paste the commit id 
git push --force                  # making changes at remote repo
```

### Check how many branches
```
git branch -a                     # check how many branches
git status                        # check which branch you're on
```

### git tagging 
<a href=https://git-scm.com/book/en/v2/Git-Basics-Tagging>source</a>
```
git tag                           # list all the available tag
git tag v1                        # create a new tag "v1" version 1
git push origin --tags            # push all tags to remote repo, by default tags are not pushed
```

### git fetch, git merge, git pull
`git fetch` + `git merge` = `git pull` 
If you don't have any conflict, you can do `git pull` to accomplish two jobs. But even if there's a conflict, `git pull` will notify you the merge conflict and you need to resolve the issue. 

### Git merge conflict
Typically when there's a conflict in the file., i.e., the same file modified by either different users or the same user in different branches try to merge into the master, `merge conflict` occur. 
```
<<<<< HEAD

=======

>>>>> new branch 
````
the content above the divider `======` is the content in current branch. If you're in master branch, the content belongs to the file in the master branch. The content below the divider is the content modified in the same file from different user or another branch. To resolve the conflict, you'd remove `<<<<<< HEAD`, `=======`, `>>>>>> new branch`, 3 merge conflicts indicators. You can either keep the original content above the divider, or keep the new content below the divider or, remove both and completely add a new content here. As long as you remove those `3` merge conflict indicators, you resolve the conflict. Then add the fixed file, and commit. 
```
git add myfile.txt
git commit -m "fixed merge conflicts"
```

### Get the latest on remote branch 

If you clone the branch and work on the branch locally and make some changes. Someone also updated the same branch on git repo. So you want to pull the latest branch from the repo to your local work station. You need to `stash` your changes until you can pull. 

```
git clone -b remote_branch https://git.myrepository.com/myportfolio.git

## work on remote_branch locally, make some changes

git stash
git pull origin remote_branch
```

## Working on a repo from web and updating locally
 
### 1. Find the git repo that you want to work on. Git clone locally. 
```
git clone https://github.com/kckenneth/Commands.git
``` 
 
If cloning the branch 
```
git clone -b myBranch https://github.com/kckenneth/Commands.git
```

### 2. Work on `git.md`, i.e, update some commands. 
```
cd Commands
git checkout -b myBranch                       # checking out to a new branch `myBranch`
vi git.md                                      # add some text 
git add git.md
git commit -m "added more git commands"
git push origin myBranch                       # pushing the branch to remote repo 
```
 
### 3. Remote origin (online git repo)
1. You'd see there's a commit in the online git repo. You need to click drop down menu to see the branch `myBranch`.  
2. Submit `pull request` on your `myBranch` with at least one reviewer selection on the right side.  
3. If the request is approved, you can merge the branch to master branch.  
4. Delete the branch after merging.  

### 4. Update locally 
```
git checkout master 
git pull -p                    # update from origin and prune all branches, i.e., deleted branch will be deleted locally 
git branch -d myBranch         # delete local myBranch 
```
 
### 5. Delete remote branch 
```
git checkout -b myBranch 
git push origin myBranch              # pushing a local branch to remote origin
git push origin --delete myBranch     # delete myBranch in remote git repo 
git branch -d myBranch                # delete myBranch locally 
```

## Checking commit history 
 
 Sometimes you want to know a specific strong or line added or removed in a specific file. 
 
 ```
 git log -p -S "movie_watch_online_4" us_web.jabba
 ```

## Reverting to the previous commit 

There's a particular commit on the branch in the remote repo that you want to work on, this is what you need to do. 
1. git clone the remote branch locally
2. search which commit you want to revert to
3. revert to the commit by commit ID

```
git clone -b remote_branch https://github.com/kckenneth/Commands.git
cd Commands
git status         # can check the branch
git log            # check which commit you want to revert to
git reset --hard 0accdefghi3a034abba82388bc3804ead1a9179ef
```


 


