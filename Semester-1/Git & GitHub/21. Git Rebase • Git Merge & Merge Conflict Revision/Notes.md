# Git Rebase • Git Merge & Merge Conflict Revision
---
# 1. Git Merge

## Definition

**Git Merge** is used to **combine the changes of one branch into another branch**.

## Explanation

Suppose we have a `main` branch and a `feature` branch:

```text
A---B---C  main
     \
      D---E  feature
```

If we want to bring the changes of `feature` into `main`:

```bash
git switch main
git merge feature
```

Possible result:

```text
      D---E
     /     \
A---B---C---M  main
```

Here, `M` is a **merge commit**.

## Important Point

> You must switch to the branch **into which** you want to merge.

```bash
git switch main
git merge feature
```

Means:

> **Merge `feature` into `main`.**

## Advantages of Merge

* Preserves the existing commit history.
* Does not rewrite existing commits.
* Safe and commonly used for shared branches.
* Makes it clear that two branches were combined.

---

# 2. Merge Conflict

## Definition

A **merge conflict** occurs when Git cannot automatically combine changes from two branches.

## When Does It Happen?

Usually when two branches modify the **same line or same part of a file differently**.

Example:

```text
main:
Hello Student

feature:
Hello Developer
```

Git cannot automatically decide which version should remain.

## Conflict Representation

Git may show:

```text
<<<<<<< HEAD
Hello Student
=======
Hello Developer
>>>>>>> feature
```

You must manually decide the final content.

## How to Resolve a Merge Conflict

Start the merge:

```bash
git merge feature
```

If a conflict occurs:

```bash
git status
```

Then:

1. Open the conflicted file.
2. Choose/fix the required content.
3. Remove the conflict markers.
4. Stage the resolved file:

```bash
git add .
```

5. Complete the merge:

```bash
git commit
```

## Conflict Flow

```text
git merge
    ↓
Conflict
    ↓
git status
    ↓
Fix the file
    ↓
git add .
    ↓
git commit
```

### Important

For a merge conflict:

> **Fix → `git add` → `git commit`**

---

# 3. Git Rebase

## Definition

**Git Rebase** is used to **move/replay the commits of one branch on top of another branch**.

It is mainly used to keep Git history **clean and linear**.

## Example

Before rebase:

```text
A---B---C  main
     \
      D---E  feature
```

Run:

```bash
git switch feature
git rebase main
```

After rebase:

```text
A---B---C---D'---E'  feature
```

`D'` and `E'` are newly created commits because Git replayed the original commits on the new base.

## Important Point

> **Rebase rewrites history.**

Therefore, the commit hashes of the replayed commits change.

---

# 4. Advantages of Rebase

### 1. Cleaner History

It can change a complicated history into a straight line:

```text
A---B---C---D'---E'
```

### 2. Easier to Read

The project history becomes easier to understand because there are usually fewer unnecessary merge commits.

### 3. Keeps Feature Branch Updated

You can bring the latest changes from `main` into your feature branch.

### 4. Useful Before Creating/Merging a PR

A developer can update their feature branch with the latest `main` changes before the feature is merged.

## Important Warning

Because rebase rewrites history:

> **Avoid rebasing a shared/public branch unless your team agrees to it.**

---

# 5. Merge vs Rebase

| Feature         | Merge                       | Rebase                          |
| --------------- | --------------------------- | ------------------------------- |
| Meaning         | Combines two branches       | Replays commits on a new base   |
| History         | Preserves existing history  | Rewrites history                |
| Merge commit    | May create one              | Usually does not create one     |
| Commit hashes   | Existing hashes remain same | Replayed commits get new hashes |
| History style   | Can be non-linear           | Usually linear                  |
| Shared branches | Generally safer             | Should be used carefully        |
| Main purpose    | Combine branches            | Keep history clean/linear       |
| Easy memory     | **Join**                    | **Replay**                      |

## Visual Difference

### Merge

```text
      D---E
     /     \
A---B---C---M
```

### Rebase

```text
A---B---C---D'---E'
```

## Easy Way to Remember

> **Merge = Join the histories**

> **Rebase = Replay the commits**

---

# 6. Why Is Rebase Used in Real Life?

Imagine you are working on a login feature:

```text
A---B  main
     \
      C---D  feature-login
```

While you are working, another developer adds changes to `main`:

```text
A---B---E---F  main
     \
      C---D  feature-login
```

Your feature branch is now behind the latest `main`.

You can update it using:

```bash
git switch feature-login
git rebase main
```

Result:

```text
A---B---E---F---C'---D'
```

Now your feature commits are based on the latest `main`.

## Real-Life Benefits

Rebase is useful when:

* `main` has received new changes while you are working.
* You want your feature branch to contain the latest `main`.
* You want a cleaner, linear history.
* You want to reduce unnecessary merge commits.
* You want to prepare your feature branch before merging it.

---

# 7. `git fetch origin`

## Definition

```bash
git fetch origin
```

`git fetch` downloads the latest information and commits from the remote repository.

It updates remote-tracking branches such as:

```text
origin/main
origin/feature-login
```

### Important

`git fetch` **does not change your current branch's files**.

It only gets the latest information from the remote repository.

## Example

Suppose GitHub has:

```text
A---B---C---D  origin/main
     \
      E---F    feature-login
```

Your local repository currently knows:

```text
A---B---C
     \
      E---F    feature-login
```

Run:

```bash
git fetch origin
```

Now your local repository knows about the latest remote `main`:

```text
A---B---C---D  origin/main
     \
      E---F    feature-login
```

Your `feature-login` branch itself has **not changed yet**.

---

# 8. What Does `origin/main` Mean?

```text
origin
   ↓
Remote repository name

main
   ↓
Branch name
```

Therefore:

```text
origin/main
```

means:

> The `main` branch of the remote repository named `origin`.

Usually:

```text
origin = GitHub remote repository
```

So:

```bash
git rebase origin/main
```

means:

> Replay my current branch's commits on top of the remote `main` branch.

---

# 9. `git fetch origin` + `git rebase origin/main`

These commands are commonly used together to update a feature branch with the **latest remote `main`**.

```bash
git fetch origin
git rebase origin/main
```

---

# 10. Real-Life Scenario — Updating a Feature Branch

Imagine you are working on a login feature.

Your branch is:

```text
feature-login
```

Initially:

```text
A---B  main
     \
      C---D  feature-login
```

While you are working, another developer pushes new changes to GitHub's `main`:

```text
A---B---E---F  origin/main
     \
      C---D    feature-login
```

You want to update your feature branch.

## Step 1 — Switch to Your Feature Branch

```bash
git switch feature-login
```

## Step 2 — Get Latest Remote Information

```bash
git fetch origin
```

Now:

```text
A---B---E---F  origin/main
     \
      C---D    feature-login
```

## Step 3 — Rebase Onto Latest Remote Main

```bash
git rebase origin/main
```

Git replays `C` and `D` on top of `F`.

Result:

```text
A---B---E---F---C'---D'  feature-login
             |
          origin/main
```

### What Happened?

The original:

```text
C---D
```

was replayed as:

```text
C'---D'
```

Your feature branch is now based on the latest remote `main`.

---

# 11. Why Use `fetch` Before Rebase?

Instead of rebasing on an old local `main`:

```bash
git rebase main
```

you can first get the latest remote changes:

```bash
git fetch origin
git rebase origin/main
```

This allows you to rebase onto the **latest fetched remote `main`**.

### Easy Memory

```text
git fetch origin
       ↓
Get latest remote information
       ↓
git rebase origin/main
       ↓
Replay feature commits on latest remote main
```

---

# 12. Git Rebase Conflict

Rebase can also create conflicts.

Suppose:

```bash
git switch feature
git rebase origin/main
```

Git tries to replay your commits but finds conflicting changes.

You may see:

```text
CONFLICT
```

## Step 1: Check the Conflict

```bash
git status
```

## Step 2: Fix the Conflicted Files

Remove the conflict markers and keep the correct content.

## Step 3: Stage the Resolved Files

```bash
git add .
```

## Step 4: Continue the Rebase

```bash
git rebase --continue
```

If another conflict occurs, repeat the process.

## Conflict Flow

```text
git rebase
    ↓
Conflict
    ↓
git status
    ↓
Fix files
    ↓
git add .
    ↓
git rebase --continue
    ↓
Another conflict?
    ↓
Repeat
```

---

# 13. `git rebase --continue`

## Definition

`--continue` tells Git:

> **"I have resolved the conflict. Continue the rebase."**

Command:

```bash
git rebase --continue
```

### Simple Example

Suppose:

```bash
git rebase origin/main
```

causes a conflict.

First:

```bash
git status
```

Fix the conflicted file.

Then:

```bash
git add Student.txt
```

Finally:

```bash
git rebase --continue
```

Git continues replaying the remaining commits.

### Remember

```text
--continue = Keep going
```

---

# 14. `git rebase --abort`

## Definition

`--abort` cancels the current rebase and returns the branch to the state it was in before the rebase started.

Command:

```bash
git rebase --abort
```

## Simple Example

Suppose you start:

```bash
git rebase origin/main
```

and several conflicts occur.

You decide that you do not want to continue.

Run:

```bash
git rebase --abort
```

Your branch returns to its previous state.

Before rebase:

```text
A---B---C  main
     \
      D---E  feature
```

After:

```bash
git rebase --abort
```

The feature branch returns to:

```text
A---B---C  main
     \
      D---E  feature
```

### Remember

```text
--abort = Cancel rebase
```

---

# 15. `git rebase --skip`

## Definition

`--skip` tells Git to **skip the current commit being replayed** and continue with the next commit.

Command:

```bash
git rebase --skip
```

## Simple Example

Suppose your feature branch has:

```text
A---B---C---D  main
     \
      E---F---G  feature
```

During rebase, Git is currently replaying commit `F`.

You discover that the changes from `F` are **already present in `main`**.

You don't need to replay `F`.

Run:

```bash
git rebase --skip
```

Git skips `F` and continues with `G`.

```text
E
↓
F  ← Current commit
↓
git rebase --skip
↓
G  ← Continue with next commit
```

### Important

Use `--skip` only when you are sure that the current commit is unnecessary or its changes are already present.

### Remember

```text
--skip = Skip current commit
```

---

# 16. `--continue` vs `--abort` vs `--skip`

| Command                 | Simple Meaning | When to Use                            |
| ----------------------- | -------------- | -------------------------------------- |
| `git rebase --continue` | Continue       | After resolving a conflict             |
| `git rebase --abort`    | Cancel         | When you want to stop the rebase       |
| `git rebase --skip`     | Skip           | When the current commit is unnecessary |

### Easy Memory Trick

```text
CONTINUE → Keep going
ABORT    → Cancel
SKIP     → Ignore current commit
```

---

# 17. What Happens After a Successful Rebase?

After a successful rebase, your feature branch may contain **new commit IDs**.

Before rebase:

```text
A---B---C---D  main
     \
      E---F    feature-login
```

After rebase:

```text
A---B---C---D---E'---F'  feature-login
```

Because `E` and `F` were replayed, they became:

```text
E'---F'
```

with new commit IDs.

## If the Branch Was Already Pushed

If `feature-login` was already pushed to GitHub before the rebase, a normal push may be rejected because the remote branch still has the old history.

You may need:

```bash
git push --force-with-lease origin feature-login
```

---

# 18. `git push --force-with-lease`

Command:

```bash
git push --force-with-lease origin <branch_name>
```

Example:

```bash
git push --force-with-lease origin feature-login
```

### One-Line Description

> **`--force-with-lease` safely force-pushes rewritten history while checking that the remote branch has not unexpectedly changed.**

Use it when a previously pushed feature branch has been rebased and needs to be updated on the remote.

---

# 19. Complete Rebase Workflow

A common real-world workflow is:

```bash
# 1. Switch to your feature branch
git switch feature-login

# 2. Get the latest remote information
git fetch origin

# 3. Rebase onto the latest remote main
git rebase origin/main

# 4. If there is a conflict:
# Fix the files

git add .

# 5. Continue the rebase
git rebase --continue

# 6. After successful rebase
git push --force-with-lease origin feature-login
```

## Workflow

```text
git switch feature-login
          ↓
git fetch origin
          ↓
git rebase origin/main
          ↓
     Conflict?
      /     \
    Yes      No
     ↓        ↓
 Fix files   Rebase
     ↓       successful
 git add .      ↓
     ↓       Push branch
git rebase      ↓
--continue   --force-with-lease
```

---

# 20. Complete Real-Life Example

Imagine you are developing a **Login System**.

Your branch:

```text
feature-login
```

Your teammate has updated `main` on GitHub.

## Step 1 — Switch to Feature Branch

```bash
git switch feature-login
```

## Step 2 — Get Latest Remote Information

```bash
git fetch origin
```

## Step 3 — Rebase Onto Latest Remote Main

```bash
git rebase origin/main
```

## Step 4 — If There Is a Conflict

Check:

```bash
git status
```

Fix the files.

Then:

```bash
git add .
git rebase --continue
```

If another conflict occurs, repeat the same process.

## Step 5 — If You Want to Cancel

```bash
git rebase --abort
```

## Step 6 — If a Commit Is Unnecessary

```bash
git rebase --skip
```

## Step 7 — After Successful Rebase

If the branch was already pushed:

```bash
git push --force-with-lease origin feature-login
```

---

# 21. Complete Rebase Flow

```text
                  Start
                    ↓
        git switch feature-login
                    ↓
          git fetch origin
                    ↓
        git rebase origin/main
                    ↓
              Conflict?
             /         \
           Yes          No
            ↓            ↓
        Fix files      Rebase
            ↓         successful
        git add .
            ↓
    git rebase --continue
            ↓
       Another conflict?
        /           \
      Yes            No
       ↓              ↓
     Repeat      Rebase complete
                       ↓
       git push --force-with-lease
```

---

# 22. Final Quick Revision

## Git Merge

```text
MERGE
↓
Combines branches
↓
May create merge commit
↓
Preserves existing history
```

## Merge Conflict

```text
git merge
    ↓
Conflict
    ↓
Fix files
    ↓
git add .
    ↓
git commit
```

## Git Rebase

```text
REBASE
↓
Replays commits onto a new base
↓
Usually creates linear history
↓
Rewrites history
```

## Rebase With Remote Main

```bash
git fetch origin
git rebase origin/main
```

## Rebase Conflict

```bash
git status
# Fix files
git add .
git rebase --continue
```

## Cancel Rebase

```bash
git rebase --abort
```

## Skip Current Commit

```bash
git rebase --skip
```

## Push After Rebase

```bash
git push --force-with-lease origin <branch_name>
```

---

# 23. Most Important Points

* **Merge → Combine branches**
* **Merge Conflict → Git cannot automatically combine changes**
* **Rebase → Replay commits on a new base**
* **Merge → Preserves existing commit history**
* **Rebase → Rewrites commit history**
* **Rebase → Useful for keeping feature branches updated with `main`**
* **`git fetch origin` → Gets the latest remote information**
* **`origin/main` → Remote `main` branch**
* **`git rebase origin/main` → Replays feature commits on the latest fetched remote `main`**
* **`--continue` → Continue after resolving a conflict**
* **`--abort` → Cancel the rebase**
* **`--skip` → Skip the current commit**
* **After rebasing a previously pushed branch → `git push --force-with-lease` may be required**

## Final Memory Trick

```text
MERGE
→ JOIN

REBASE
→ REPLAY

FETCH
→ GET LATEST REMOTE INFORMATION

CONTINUE
→ KEEP GOING

ABORT
→ CANCEL

SKIP
→ SKIP CURRENT COMMIT

FORCE-WITH-LEASE
→ SAFELY UPDATE REWRITTEN REMOTE HISTORY
```

