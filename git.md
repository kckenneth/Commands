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



