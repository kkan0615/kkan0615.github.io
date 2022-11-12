---
title: Alternative way of "git checkout"
author: Youngjin Kwak
date: 2022-11-10 18:21:00 +0800
categories: [git]
tags: [git]
image:
path: ../images/git-logo.jpg
width: 800
height: 500
alt: git-logo.
---
---
# What is "checkout"
```checkout``` is used for switch branch or restore working tree files.
```
# Move to specific branch
git checkout <branch-name>
# Create new branch and then move to that branch
git checkout -b <new-branch>
```
# Alternative
```checkout``` command is seperated to two commands, ```switch``` and ```restore```. These commands are introduced Git v2.23.
# ```switch``` command
```switch``` command helps to switch specific branch.
```
git switch <branch-name>
```
**branch-name** is local or remote branch

## How to create new branch?
```branch``` command allows you to create new branch with specific name.
```
git branch <new-branch>
```
or you can use ```switch``` with ```-c``` or ```--create``` option
```
git switch -c <new-branch>
git switch -create <new-branch>
```
## Useful options
### ```--discard-changes```, ```--f``` or ```force```
Proceed even if the index or the working tree differs from HEAD
```
git switch <branch-name> --discard-changes
```
### ```-m``` or ```--merge```
It will try a three-way merge. After three-way merge, ```git diff``` would show you what changes you made
```
git switch <branch-name> -m
git switch <branch-name> --merge
```
### ```-```
Switch back to the previous branch.
```
git swtich -
```

# ```restore``` command
```restore``` command helps to unstage or event discard uncommited local changes.
In official document, it's explained as "Restore working tree files"
```
# Restore all files in current branch
git restore .
```
## Useful options
### ```--staged```
It will only restore the index.html file
```
git restore --staged index.html
```
### ````--staged``` and ```*```
With ```*```, you can remove multiple files with following extension
```
git restore --staged *.css
```

# Ref
- [Do not use ‘git checkout’ anymore - TheDevStory](https://medium.com/@materokatti/do-not-use-git-checkout-anymore-aa73c0a43c13)
- [git-checkout - git official document](https://git-scm.com/docs/git-checkout)
- [git-switch - git official document](https://git-scm.com/docs/git-switch)
- [git-restore - git official document](https://git-scm.com/docs/git-restore)
- [git-restore - Tower](https://www.git-tower.com/learn/git/commands/git-restore)

# Support
