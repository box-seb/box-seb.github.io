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
