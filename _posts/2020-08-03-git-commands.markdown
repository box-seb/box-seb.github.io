---
layout: post
title:  "Git commands I like"
date:   2020-08-03 19:03:04 +1200
---


Diff for not staged changes
```
git diff
```

Diff for staged changes
```
git diff --staged
```

Unstage any staged changes for the given file
```
git reset -- <filePath>
```

Back to previous branch
```
git checkout -
```

Stash changes
```
git stash
```

Pop stashed changes
```
git stash pop
```

# Aliases

```
alias.com=checkout
alias.st=status
alias.coms=log --pretty=oneline origin..HEAD
alias.co=checkout
alias.com=checkout master
alias.ce=config --global -e
alias.up=!git pull --rebase --prune $@ && git submodule update --init --recursive
alias.cob=checkout -b
alias.cm=commit -m
alias.save=!git add -A && git commit -m 'WIP'
alias.undo=reset HEAD~1 --mixed
alias.amend=commit --amend --no-edit
alias.wipe=!git add -A && git commit -qm 'WIPE SAVEPOINT' && git reset HEAD~1 --hard
alias.p=push
alias.pl=push -u origin HEAD
alias.pf=push -f
alias.branch-clean=!f() { git checkout master }
alias.a=config --list | grep alias
alias.rbi=rebase -i
```

# Worktree

Git worktree allows to work with the same repository on multiple branches at the same time without switching them. Every [worktree](https://git-scm.com/docs/git-worktree) is located in dedicated folder therefore it is enough to switch working folder to switch between branches. 

Run both commands below in the root folder of your repo:
- Create a work tree:
  
```
git worktree add FolderNameOfYourWorktree -b BranchName
```

- [Remove](https://git-scm.com/docs/git-worktree#Documentation/git-worktree.txt-remove) a worktree:
  
```
git worktree remove -f FolderNameOfYourWorktree
```
