    GIT IS AN OPEN SOURCE VERSION CONTROL SYSTEM(VCS) 
    
# Chapter 2. Collaborating with issues and PR(pull requests) #  

## Table of Contents ##  


### Syncing a Fork ###  

1-0.  

Check and configuring a remote upstream repository in Git with the original repository for sync changes you make in fork.  


1-1. 
 ```bash 
 $  git remote -v #List the current configured remote repository 
origin  https://github.com/YOUR_USERNAME/YOUR_FORK.git (fetch)
origin  https://github.com/YOUR_USERNAME/YOUR_FORK.git (push)  
  ```  

1-2. 
```bash  
$ git remote add upstream https://github.com/ORIGINAL_OWNER/ORIGINAL_REPOSITORY.git  
#specify a new remote upstream repository for sync the fork  
```   

1-3.  
```bash 
 $  git remote -v  
 #Verify the new upstream repository you have specified for you fork  
 origin    https://github.com/YOUR_USERNAME/YOUR_FORK.git (fetch)
 origin    https://github.com/YOUR_USERNAME/YOUR_FORK.git (push)
 upstream  https://github.com/ORIGINAL_OWNER/ORIGINAL_REPOSITORY.git (fetch)
 upstream  https://github.com/ORIGINAL_OWNER/ORIGINAL_REPOSITORY.git (push) 
```  

2-0.  

Sync a fork  

2-1.  
```bash 
$ git fetch upstream  
#Fetch the branches from upstream repository.Commits to `master` will be stored in a local branch `upstream\master`.  
From https://github.com/ORIGINAL_OWNER/ORIGINAL_REPOSITORY
 * [new branch]      master     -> upstream/master   
```  

2-2.  
```bash  
$ git checkout master  
#check out your fork's local `master` branch  
Switched to branch 'master'
```  

2-3.  
```bash  
$ git merge upstream/master  
# merge the change from `upstream/master` into your local `master` branch. This brings your fork's `master` branch into sync with the upstream repository, without losing your local changes.    
Updating a422334..5dff0f  
Fast-forward  
  README                      |    9 -------
  README.md                   |    7 +++++  
  2 files changed, 7 insertions (+), 9 deletions (-)  
  delete mode 100644 README  
  create mode 100644 README.md  
```  

2-4.  
```bash  
$ git merge upstream/master  
# Git will instead perform a "fast-forward", if your local branch didn't have any unique commits.    
Updating 3e93da..17c67ad  
Fast-forward  
 README.md                 |  5 +++-- 
 1 file changed, 3 insertions(+), 2 deletions(-)  
```  

2-5.  
After syncing youtr fork only updating your local repository, to update your fork to github, you must **push** your changes.  
