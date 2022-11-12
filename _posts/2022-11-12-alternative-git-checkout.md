---
title: Git: Alternative way of "git checkout"
author: Youngjin Kwak
date: 2022-11-12 12:10:00 +0800
categories: [git]
tags: [git]
image:
  path: ../images/git-logo.jpg
  width: 800
  height: 500
  alt: git-logo
---
---
# What is ```checkout```
```checkout``` is used for switch branch or restore working tree files.
```shell
# Move to specific branch
git checkout <branch-name>
# Create new branch and then move to that branch
git checkout -b <new-branch>
```

# Alternative
```checkout``` command is seperated to two commands, ```switch``` and ```restore```. These commands are introduced Git v2.23.
# ```switch``` command
```switch``` command helps to switch specific branch.
```shell
git switch <branch-name>
```
**branch-name** is local or remote branch

## How to create new branch?
```branch``` command allows you to create new branch with specific name.
```
git branch <new-branch>
```
or you can use ```switch``` with ```-c``` or ```--create``` option
```shell
git switch -c <new-branch>
git switch -create <new-branch>
```
## Useful options
### ```--discard-changes```, ```--f``` or ```force```
Proceed even if the index or the working tree differs from HEAD
```shell
git switch <branch-name> --discard-changes
```
### ```-m``` or ```--merge```
It will try a three-way merge. After three-way merge, ```git diff``` would show you what changes you made
```shell
git switch <branch-name> -m
git switch <branch-name> --merge
```

### ```-```
Switch back to the previous branch.
```shell
git swtich -
```

# ```restore``` command
```restore``` command helps to unstage or event discard uncommited local changes.
In official document, it's explained as "Restore working tree files"
```shell
# Restore all files in current branch
git restore .
```
## Useful options
### ```--staged```
It will only restore the index.html file
```shell
git restore --staged index.html
```
### ````--staged``` and ```*```
With ```*```, you can remove multiple files with following extension
```shell
git restore --staged *.css
```


# Ref
- [Do not use ‘git checkout’ anymore - TheDevStory](https://medium.com/@materokatti/do-not-use-git-checkout-anymore-aa73c0a43c13)
- [git-checkout - git official document](https://git-scm.com/docs/git-checkout)
- [git-switch - git official document](https://git-scm.com/docs/git-switch)
- [git-restore - git official document](https://git-scm.com/docs/git-restore)
- [git-restore - Tower](https://www.git-tower.com/learn/git/commands/git-restore)

# Support
[!["Buy Me A Coffee"](https://www.buymeacoffee.com/assets/img/custom_images/orange_img.png)](https://www.buymeacoffee.com/youngjinkwak)
