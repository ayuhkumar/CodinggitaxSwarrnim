# Git Rebase • Git Merge & Merge Conflict Revision

## 1. Git Merge

### Definition

**Git Merge** is used to **combine the changes of one branch into another branch**.

### Explanation

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

### Important Point

> You must switch to the branch **into which** you want to merge.

```bash
git switch main
git merge feature
```

Means: **Merge `feature` into `main`.**

### Advantages of Merge

* Preserves the existing commit history.
* Does not rewrite existing commits.
* Safe and commonly used for shared branches.
* Makes it clear that two branches were combined.

---

# 2. Merge Conflict

### Definition

A **merge conflict** occurs when Git cannot automatically combine changes from two branches.

### When does it happen?

Usually when two branches modify the **same line or same part of a file differently**.

Example:

```text
main:
Hello Student

feature:
Hello Developer
```

Git cannot decide which version should remain.

### Conflict Representation

Git may show:

```text
<<<<<<< HEAD
Hello Student
=======
Hello Developer
>>>>>>> feature
```

You must manually decide the final content.

### How to Resolve a Merge Conflict

```bash
git merge feature
```

If conflict occurs:

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

### Conflict Flow

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

### Definition

**Git Rebase** is used to **move/replay the commits of one branch on top of another branch**.

It is mainly used to keep the Git history **clean and linear**.

### Example

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

### Important Point

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

### Important Warning

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

### Visual Difference

**Merge:**

```text
      D---E
     /     \
A---B---C---M
```

**Rebase:**

```text
A---B---C---D'---E'
```

### Easy Way to Remember

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

### Real-Life Benefits

Rebase is useful when:

* `main` has received new changes while you are working.
* You want your feature branch to contain the latest `main`.
* You want a cleaner, linear history.
* You want to reduce unnecessary merge commits.
* You want to prepare your feature branch before merging it.

---

# 7. Git Rebase Conflict

Rebase can also create conflicts.

Suppose:

```bash
git switch feature
git rebase main
```

Git tries to replay your commits but finds conflicting changes.

You may see:

```text
CONFLICT
```

### Step 1: Check the conflict

```bash
git status
```

### Step 2: Fix the conflicted files

Remove conflict markers and keep the correct content.

### Step 3: Stage the resolved files

```bash
git add .
```

### Step 4: Continue the rebase

```bash
git rebase --continue
```

If another conflict occurs, repeat the process.

```text
Conflict
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

# 8. `git rebase --continue`

### Definition

`--continue` tells Git:

> **"I have resolved the conflict. Continue the rebase."**

Command:

```bash
git add .
git rebase --continue
```

### Remember

```text
--continue = Keep going
```

---

# 9. `git rebase --abort`

### Definition

`--abort` cancels the current rebase and returns the branch to the state it was in before the rebase started.

Command:

```bash
git rebase --abort
```

Use it when:

* The rebase became too complicated.
* You do not want to continue.
* You want to start the rebase again later.

### Remember

```text
--abort = Cancel rebase
```

---

# 10. `git rebase --skip`

### Definition

`--skip` tells Git to **skip the current commit being replayed** and continue with the next commit.

Command:

```bash
git rebase --skip
```

Use it only when you are sure that the current commit is unnecessary or its changes are already present elsewhere.

### Remember

```text
--skip = Skip current commit
```

---

# 11. Rebase Conflict — Quick Revision

| Command                 | Purpose                             |
| ----------------------- | ----------------------------------- |
| `git rebase --continue` | Continue after resolving a conflict |
| `git rebase --abort`    | Cancel the entire rebase            |
| `git rebase --skip`     | Skip the current commit             |

### Easy Memory Trick

```text
CONTINUE → Keep going
ABORT    → Cancel
SKIP     → Ignore current commit
```

---

# 12. Final Quick Revision

```text
MERGE
↓
Combines branches
↓
May create merge commit
↓
Preserves existing history
```

```text
REBASE
↓
Replays commits onto a new base
↓
Usually creates linear history
↓
Rewrites history
```

### Conflict Resolution

**Merge Conflict:**

```bash
git status
# Fix files
git add .
git commit
```

**Rebase Conflict:**

```bash
git status
# Fix files
git add .
git rebase --continue
```

### Most Important Points

* **Merge → Combine branches**
* **Merge Conflict → Git cannot automatically combine changes**
* **Rebase → Replay commits on a new base**
* **Merge → Preserves commit history**
* **Rebase → Rewrites commit history**
* **Rebase → Useful for keeping feature branches updated with `main`**
* **`--continue` → Continue**
* **`--abort` → Cancel**
* **`--skip` → Skip current commit**
