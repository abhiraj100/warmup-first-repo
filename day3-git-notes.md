# Day 3 — Git Learning Notes

**Topics covered:** Git workflow, core commands, and FloCard branching strategy

## 1. Why Git Matters

- **Version history** — every change is recorded with who made it, when, and why (via the commit message), so nothing is ever silently lost
- **Team collaboration** — multiple engineers can work on the same codebase simultaneously without overwriting each other's work
- **Safety net** — because history is preserved, it's always possible to inspect, compare, or revert to an earlier state of the code
- **Parallel work** — branching lets different features, fixes, and experiments be developed independently of the stable codebase
- **Accountability & traceability** — commit history creates an audit trail that's invaluable for debugging

## 2. Core Commands

| Command | What it does |
|---|---|
| `git add <file>` | Stages a file — moves changes into the staging area, marking them ready to commit |
| `git commit -m "message"` | Saves everything staged as a permanent snapshot in the repository's history |
| `git push` | Uploads local commits to the remote repository (e.g. GitHub) |
| `git pull` | Downloads and merges the latest changes from the remote into the local branch |
| `git merge` | Combines changes from one branch into another (e.g. feature branch into `dev`) |

**Staging vs. committing:** editing a file only changes the working directory. `git add` moves that change into a preview list (staging area) of what the next commit will contain. `git commit` then takes a permanent snapshot of exactly what's staged — this lets you build commits deliberately instead of committing everything at once.

## 3. Resolving Merge Conflicts (Basics)

A merge conflict happens when Git can't automatically combine changes — usually because two branches edited the same lines of the same file differently. Git marks the conflicting section directly in the file:

```
<<<<<<< HEAD
your current branch's version of the code
=======
the incoming branch's version of the code
>>>>>>> feature/branch-name
```

To resolve: read both versions, decide the correct final code, remove the conflict markers, then stage and commit the resolved file. Test the code before pushing.

## 4. Branching Strategy (FloCard)

| Branch | Purpose | Stability |
|---|---|---|
| `main` | Production-ready code only | Always stable and deployable |
| `dev` | Integration branch for completed features | Should build/pass tests, may contain unreleased work |
| `feature/*` | One branch per feature/fix/task, created off `dev` | Can be unstable — active development happens here |

**Typical flow:** create `feature/*` from `dev` → commit work regularly → push the branch → open a pull request into `dev` → get it reviewed and merged → periodically merge stable `dev` into `main` to cut a release.

## 5. Key Takeaways

- Git protects work, enables collaboration, and creates a reliable history of the project
- Every commit is a timestamped, attributable snapshot that can be viewed, compared, or reverted
- Branches let people work in parallel; `push`/`pull` keeps everyone synchronized
- Code review happens through pull requests before merging into `dev`/`main`
- Keeping `main` clean and using short-lived `feature/*` branches keeps the codebase stable
