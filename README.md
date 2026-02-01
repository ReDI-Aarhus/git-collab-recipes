# Recipe Book — GitHub Collaboration Workshop

Welcome! You and your team will collaborate on this recipe collection to
practice real-world GitHub workflows.

## Before You Start

1. **Fork** this repository to your own GitHub account (click **Fork** in the top-right corner)
   > Important: uncheck **"Copy the main branch only"** so your fork includes all branches
2. Clone your fork locally:
   ```bash
   git clone https://github.com/your-username/git-collab-recipes
   cd git-collab-recipes
   ```
3. Verify you have all branches:
   ```bash
   git fetch --all
   git branch -r   # you should see fix/improve-formatting and feat/beverages
   ```
4. Read `CONTRIBUTING.txt` — it defines the rules your team follows.
5. Browse the existing recipes in `recipes/` to understand the format.

---

## Challenges

### Challenge 1 — Best Practices: Your First Contribution

**Goal**: Add a new recipe using proper team conventions.

**Steps**:
1. Create a branch: `git checkout -b feat/yourname/recipe-name`
2. Add a new recipe `.txt` file in `recipes/` — follow the format of existing recipes
3. Add your name to `CONTRIBUTORS.txt` (append at the end)
4. Add your recipe to `RECIPES_INDEX.txt` in alphabetical order by filename
5. Commit: `git add . && git commit -m "feat: add [recipe name] recipe"`
6. Push and open a Pull Request on GitHub with a clear title and description

> Read `CONTRIBUTING.txt` for the exact branch naming and commit format.

Done when: Your PR is open on GitHub with correct branch name, commit message, and description.

---

### Challenge 2 — Code Review

**Goal**: Review a teammate Pull Request and give useful feedback.

**Steps**:
1. Go to the **Pull Requests** tab on GitHub
2. Open a teammate PR (not your own)
3. Click **Files changed** to see what they added
4. Hover over a line and click **+** to leave an inline comment
5. Submit your review: **Approve** or **Request changes** — always include a reason
6. If your PR received a review with requested changes, respond and update

Done when: You have reviewed a teammate PR and your PR has received at least one review.

---

### Challenge 3 — Merge Conflict

**Goal**: Resolve a conflict after two people edited the same file.

**Why this happens**: Everyone appends their name to `CONTRIBUTORS.txt` in
Challenge 1. When the second PR tries to merge into main, Git cannot
automatically combine both changes — it needs your help.

**Steps**:
1. After another PR merges into main, pull latest and merge into your branch:
   ```bash
   git checkout main && git pull origin main
   git checkout feat/yourname/recipe-name
   git merge main
   ```
2. Open `CONTRIBUTORS.txt` — find the conflict markers (`<<<<<<<`, `=======`, `>>>>>>>`)
3. Resolve: keep **all** names (yours and your teammates), remove the markers
4. Commit and push:
   ```bash
   git add CONTRIBUTORS.txt
   git commit -m "fix: resolve conflict in contributors list"
   ```
5. Push and merge your PR

Done when: Your PR is merged and `CONTRIBUTORS.txt` contains all team names.

---

### Challenge 4 — Stash

**Goal**: Save work in progress, handle an urgent fix, then come back.

**Scenario**: You are mid-way adding a second recipe (file created, not
committed yet). The team noticed a typo in `recipes/pasta-carbonara.txt` —
line 6 says "guancale" but it should be "guanciale". Fix it without losing
your work in progress.

**Steps**:
1. Start adding a second recipe — create the `.txt` file but do **not** commit
2. Save your work in progress:
   ```bash
   git stash push -m "wip: adding [your recipe name]"
   ```
3. Verify: `git stash list`
4. Switch to main, pull, and create a hotfix branch:
   ```bash
   git checkout main && git pull origin main
   git checkout -b fix/yourname/carbonara-typo
   ```
5. Fix the typo in `recipes/pasta-carbonara.txt` (line 6: guancale → guanciale)
6. Commit, push, open PR, and merge:
   ```bash
   git add recipes/pasta-carbonara.txt
   git commit -m "fix: correct guanciale spelling in carbonara"
   git push origin fix/yourname/carbonara-typo
   ```
7. Return to your feature branch and restore your stash:
   ```bash
   git checkout feat/yourname/second-recipe-branch
   git stash pop
   ```
8. Continue and commit your second recipe

Done when: The typo is fixed in main AND your second recipe is committed.

---

### Challenge 5a — Cherry-pick (Bonus)

**Goal**: Apply one specific commit from another branch — without merging the whole branch.

**Context**: The branch `fix/improve-formatting` has one commit that adds a
`RECIPE_TEMPLATE.txt` file. You want that file on your branch too, without
merging everything else from that branch.

**Steps**:
1. Find the SHA of the commit you want:
   ```bash
   git log origin/fix/improve-formatting --oneline
   ```
2. Apply that single commit to your current branch:
   ```bash
   git cherry-pick <SHA>
   ```
3. Verify: `RECIPE_TEMPLATE.txt` should now exist in your branch

Done when: `RECIPE_TEMPLATE.txt` appears in your branch via cherry-pick.

---

### Challenge 5b — Rebase (Bonus)

**Goal**: Update a feature branch with the latest main commits — keeping a clean, linear history.

**Context**: The branch `feat/beverages` was created before some recent
commits on main. It is behind by 3 commits. Instead of merging main into it
(which creates an extra merge commit), use rebase.

**Steps**:
1. Create a local copy to work with:
   ```bash
   git checkout -b feat/yourname-beverages origin/feat/beverages
   ```
2. Rebase onto main:
   ```bash
   git rebase main
   ```
3. Verify linear history — main commits followed by the smoothie commit on top:
   ```bash
   git log --oneline
   ```
4. Push your branch:
   ```bash
   git push origin feat/yourname-beverages
   ```

Done when: Your branch shows a linear history with all main commits followed by the smoothie commit.

---

## Quick Reference

| Concept | Command |
|---------|---------|
| Save WIP | `git stash push -m "message"` |
| List stashes | `git stash list` |
| Restore WIP | `git stash pop` |
| Cherry-pick | `git cherry-pick <sha>` |
| Rebase onto main | `git rebase main` |
| Safe force push | `git push --force-with-lease` |
