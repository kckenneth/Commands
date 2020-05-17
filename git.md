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

