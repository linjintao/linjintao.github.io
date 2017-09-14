---
layout: post
title: "Understanding Git"
date: 2017-09-13 23:34:25 +0800
comments: true
categories: 
---
## Hello Word Guide
Here is a great brief introduction about Git. You can learn the base knowledge about [Git](http://www.runoob.com/manual/git-guide/) in 5 minutes.
>+ [Git Documentation](https://git-scm.com/docs)
>+ [Git Cheat Sheet](http://www.runoob.com/manual/github-git-cheat-sheet.pdf)

## Clone The Project
To start coding, we need clone the project from server, we can use **git clone** to make a copy of the project src code.
```
$ git clone https://gitee.com/machineplayer/gitee_leetcode.git
Cloning into 'gitee_leetcode'...
```
## Branch Mange
Now we have a folder named as **gitee_leetcode**, it is tracked by git. Normally, there is a default remote branch **origin**, and the main branch **master**. Use **git branch -a** to check the branch.
```
# -a , show all the branch
$ git branch -a
* master
  remotes/origin/HEAD -> origin/master
  remotes/origin/master
```
Before we start coding, we need a new branch, so that we could revert the changes. We can also give the branch a prefix or namespace.
```
$ git branch mybranch/FeatureA
$ git checkout mybranch/FeatureA
Switched to branch 'mybranch/FeatureA'
$ git branch -a
  master
* mybranch/FeatureA
  remotes/origin/HEAD -> origin/master
  remotes/origin/master

$ git checkout master
$ git merge mybranch/FeatureA
```
**'*'** means this branch is the current working branch. Now we add a new file, and commit it.

## Remote Branch
```
$ git add github https://github.com/machineplayer/gitee_leetcode.git
# -u, up stream, src_branch:dst_branch
$ git push -u -f origin master:master

```

## Tracking The Change

The following commands show how to add a file and commit it to current branch
```
$ echo "MIT license" > license.txt
$ git status
On branch mybranch/FeatureA
Untracked files:
  (use "git add <file>..." to include in what will be committed)

    license.txt
$ git add license.txt
$ git status
On branch mybranch/FeatureA
Changes to be committed:
  (use "git reset HEAD <file>..." to unstage)

    new file:   license.txt
# edit the file again and check the status
$ echo "BSD license" > license.txt
$ git status
On branch mybranch/FeatureA
Changes to be committed:
  (use "git reset HEAD <file>..." to unstage)

    new file:   license.txt

Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git checkout -- <file>..." to discard changes in working directory)

    modified:   license.txt
$ git add license.txt & git commit -m "add and modify license"
```


## The Three Trees

| Tree | Role |
| ----- | ------ |
| Head | Last commit snapshot, next parent |
| Index | Proposed next commit snapshot |
| Working Directory | Sanbox |


## Revert The Change
+ revert branch -- git reset [--soft|mix|hard] Head~2

| Option | Effect |
| ------ | ------ |
| soft | only revert the Head tree |
| mix | Head tree and Index tree |
| hard | Head, Index and Working Directory |

+ revert file -- git checkout -- filename.txt
This command will revert the change to the last **git add** or **git commit**. "--" is needed, otherwise filename is used as branch name.



## Git Help
The most useful command is **git help**
```
$ git help reset
```

>+ [Git Book](https://git-scm.com/book/zh/v2)
>+ [Git Documentation](https://git-scm.com/doc)