## Git Feature Branch Workflow Cheat Sheet

### 1. Clone repository (first time)
```
git clone <remote-url>
cd <repo>
````

### 2. Keep main updated

```
git checkout main
git fetch origin
git pull origin main          ## merge remote changes
## OR cleaner history
git pull --rebase origin main
```

### 3. Create a feature branch

```
git checkout -b feature-xyz
```

### 4. Work locally

```
git add .
git commit -m "Implement feature xyz"
```

### 5. Sync with latest main before pushing

```
git fetch origin
git rebase origin/main        ## preferred for clean history
## OR merge if you want merge commits
git merge origin/main
```

### 6. Push branch to remote

```
git push -u origin feature-xyz
## If rebased after previous push:
git push -u origin feature-xyz --force
```

### 7. Finish work (merge to main)

**Option A — Pull Request (recommended)**

* Open PR from `feature-xyz` → `main`
* Merge via UI (fast-forward or squash)

**Option B — Merge locally**

```
git checkout main
git pull origin main
git merge feature-xyz            ## fast-forward if possible
## OR less common:
git rebase feature-xyz
git push origin main
```

### 8. Cleanup branches

```
git branch -d feature-xyz
git push origin --delete feature-xyz
git fetch --prune   ## cleanup deleted remote branches
```

### 9. Useful cleanup

```
git clean -n    ## show untracked files
git clean -f    ## delete untracked files
git clean -fd   ## delete untracked files + directories
```

### Summary

* Always update `main` before branching
* Prefer **rebase** for clean, linear history (optional)
* Push branches, open PRs, merge, then delete branches
* Use merge only if you don’t want history rewritten
