# Git command line

## Table of Contents
1. [Introduction to Git](#introduction-to-git)
2. [Setting Up Git](#setting-up-git)
    - [Working smarter not harder](#working-smarter-not-harder)
3. [Basic Git Commands](#basic-git-commands)
    - [git init](#git-init)
    - [git status](#git-status)
    - [git add](#git-add)
    - [git commit](#git-commit)
    - [git log](#git-log)
4. [Branching](#branching)
    - [git branch](#git-branch)
    - [git checkout](#git-checkout)
    - [git merge](#git-merge)
4. [Merge vs. Rebase](#merge-vs-rebase)
    - [git merge](#git-merge-1)
    - [git rebase](#git-rebase-1)
    - [Summary](#summary)
5. [Remote Repositories](#remote-repositories)
    - [git remote](#git-remote)
    - [git push](#git-push)
    - [git pull](#git-pull)
6. [Conclusion](#conclusion)

## Introduction to Git

Git is a distributed version control system that allows multiple developers to work on a project simultaneously. 
It helps you track changes, revert to previous stages, and collaborate with others.

## Setting Up Git

Before you start using Git, you need to configure it with your user information.

```bash
git config --global user.name "Your Name"
git config --global user.email "your.email@example.com"
```

### Working smarter not harder

If you don't have it installed already, I recommend you to use the .zsh shell in combination with [ohmyzsh](https://ohmyz.sh) and the git plugin. For any questions you can ask me any time. The git plugin comes with really useful aliases for the most used git commands. 

When you have it installed, you can look at all your git aliases with `alias | grep <git command>` or just `alias` for all you have active.

```bash
alias | grep "\'git"
```


## Basic Git commands

### git init

To start tracking a project with Git, you need to create a repository with 

```bash
git init
```

This command initializes a new Git repository in your current directory.

### git show


To look at the changes of a specific commit, you can just use the 'show' command. 
By default it shows you the last commit. But you can also give it a specific 
commit hash to dive into the changes of a specific commit. 

```bash
git show
```

```bash
# zsh aliases
gsh
gsps # pretty short
```

### git status

```bash
git status
```

Shows the current status of your working directory and staging area. It indicates which files have changes that are staged, unstaged, or untracked.

```bash
# zsh aliases
gst
gss # short
```

### git add

```bash
git add <filename>
```

Stages changes in <filename> for the next commit.

```bash
git add --all
```

Stages ALL changes. No matter in which dir you are currently in the repository.

```bash
# zsh aliases
gaa # add all
```

### git commit

```bash
git commit -m 'Commit message'
```

Commits all staged changes to the repo with a message describing the change. 

```bash
git commit --amend
```

Rewrites the last commit and adds all changes that are corrently staged to the last commit. 
This command can also be used to change the commit message afterwards. It is necessary to
forcly push the commit to the remote afterwards with `git push -f`

```bash
# zsh aliases
gcmsg
```

### git log

If you want to look at the commit history. Use the 'log' command.

```bash
git log
```

A pretty useful and nice to look at variation of this command is the command

```bash
git log --oneline --decorate --graph --all
```

```bash
# zsh aliases
glog
gloga # with graph
```

### git diff

If you want to see your unstaged changes you can do so by hitting

```bash
git diff
```

```bash
# zsh aliases
gd
```

## Branching

Branching allows you to create separate lines of development in your project.

### git branch

```bash
git branch <banch_name>
```

Creates a new branch called <branch_name>. To just list all local branches use the command without a branch name like

```bash
git branch
```

if you want to include all remove branches, add `-a` as an argument

```bash
git branch -a
```

To delete a branch either use the args '-d' or '-D' to delete just a merged branche or force a deletion.

```bash
# zsh aliases
gb
gba # show all
gbD # force delete
```

### git checkout

Checkout just switches the branch.

```bash
git checkout <branch_name>
```

You can also create a new branch and check it out at the same time with '-b'.

```bash
git checkout -b <branch_name>
```

```bash
# zsh aliases
gco
gcb # checkout and create 
gcm # directly checkout main branch ;)
```

### git merge

```bash
git merge <branch_name>
```

Merges the branch <branch_name> into the current branch.

```bash
# zsh aliases
gm
gms # squash (only one merge summed up merge-commit)
```

### git rebase

```bash
git rebase <branch_name>
```

Puts all new commits of the current branch onto the branch <branch_name> and rewrites commit history. 
In general you must forcly push after everytime you rewrite the commit history. 

```bash
# zsh aliases
grb
grbc # git rebase --continue
```

## Merge vs. Rebase

Certainly! Here's a short description of the differences between git merge and git rebase:

### git merge
- Purpose: Combines two branches together by creating a new "merge commit" that ties the histories of both branches.
- Process: Takes the changes from the source branch and merges them into the target branch, preserving the original commit history of both branches.
- History: The commit history will show a clear path of where branches diverged and where they were merged back together.
- Use Case: Ideal for maintaining a clear, non-linear history, especially in collaborative projects where it's important to see how and when branches were combined.

<img src="https://wac-cdn.atlassian.com/dam/jcr:4639eeb8-e417-434a-a3f8-a972277fc66a/02%20Merging%20main%20into%20the%20feature%20branh.svg?cdnVersion=2123" alt="Merging main into the feature branch" width="700">

### git rebase
- Purpose: Reapplies commits from one branch on top of another base branch, effectively rewriting history.
- Process: Takes the commits from the source branch and replays them on top of the target branch, moving the base of the source branch to the latest commit on the target branch.
- History: Creates a linear history without merge commits, as if the commits were made sequentially on top of the target branch.
- Use Case: Ideal for cleaning up a feature branch before merging it into the main branch, or when you want to keep a linear project history.

<img src="https://wac-cdn.atlassian.com/dam/jcr:3bafddf5-fd55-4320-9310-3d28f4fca3af/03%20Rebasing%20the%20feature%20branch%20into%20main.svg?cdnVersion=2123" alt="Rebasing the feature branch onto main" width="700">

### Summary
- **git merge**  is great for preserving the complete history of changes, including when branches diverge and converge.
- **git rebase** is useful for creating a cleaner, linear history, often making it easier to follow but at the cost of rewriting commit history.

Use merge when you want to keep the context of branch development clear, and use rebase when you want a simplified history.

A very useful link is the [atlassian tips page]() for merging vs. rebasing. It describes it very good imo.

## Remote Repositories

Remote repositories allow you to collaborate with others by sharing your changes.

### git remote

```bash
git remote add origin <remote_repository_URL>
```

This command adds a remote repo URL with the name 'origin'.

```bash
# zsh aliases
gra
```

### git push

```bash
git push origin <branch_name>
```

Pushes your commits to the remote repository on the branch <branch_name>.

OR - If you want to push you changes on your local branch to the corresponding branch on the remote, just `git push`

```bash
# zsh aliases
gp
gpf! # force push
```

### git pull

```bash
git pull origin <branch_name>
```

Fetches and merges changes from the remote repository to your local branch.

```bash
# zsh aliases
gl
```

## Conclusion

Congrats! You've learned the basics of using Git from the command line now. Keep practicing these commands and explore more advanced Git features as you become a real PRO with version control. 🎉

You can find this file in [Github](https://github.com/dennishenle/git-cheatsheet.git).