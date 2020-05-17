### To clone the repository from the github 
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


