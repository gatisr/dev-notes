---
layout: default
title: Git Merge Workflow
parent: DevOps
---

Fast-forward merge ensures clean linear history without merge commits:

```bash
git checkout develop
git pull
git checkout main
git pull
git merge --ff-only develop
git push
git checkout develop
```

**Why `--ff-only`?**

- Prevents accidental merge commits
- Maintains linear history
- Fails if branches diverged (forces you to rebase first)
- Cleaner git log

**If merge fails:**

```bash
git checkout develop
git rebase main
# resolve conflicts if any
git checkout main
git merge --ff-only develop
```
