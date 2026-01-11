---
layout: post
title: Git cheatsheet
date: 2026-01-11 19:37:29 +0530
author: Aarcha Paul
summary: Quick cheatsheet on git
categories: cheatsheet
thumbnail: jekyll
tags:
  - bugbounty
---
# Git cheatsheet

`git init`: Initializes a new Git repository in the current directory
`git add <filename>`: Adds specified file to the staging area
`git add .` : Adds all modified and new files to the staging area
`git commit -m "<add commit message>"` : Creates a new commit with the changes in the staging area and specifies the commit message inline
`git push` : Pushes local commits to the remote repository
`git pull`: Pulls changes from the remote repository and merges them into the current branch.
`git clone <repository url`: Clones a repository from remote server to your local machine.
`git branch`: Lists all branches in the repository.
`git branch <branch-name>` : Creates a new branch with the specified name.
`git fetch`: Fetches change from a remote repository, including new branches and commit.
`git checkout <branch-name>`: Switches to the specified branch
`git branch -r`: Lists all remote branches
`git branch -a`: Lists all local and remote branches