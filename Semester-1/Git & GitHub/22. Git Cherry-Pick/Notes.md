
# Git Cherry-Pick

## 1. What is Git Cherry-Pick?

`git cherry-pick` is used to **apply the changes of a specific commit from one branch to another branch**.

### Simple Meaning

> **🍒 Cherry-pick = Select a specific commit and apply its changes to another branch.**

Unlike `git merge`, cherry-pick does **not bring the entire branch**.

---

## 2. Simple Example

Suppose we have a Student Management System.

Initially:

```text
Student Management System
```

Create and commit the file:

```bash
git add Student.txt
git commit -m "Create Student file"
```

Now create a new branch:

```bash
git switch -c student-info
```

Add Rahul:

```text
Student Management System
Name: Rahul
```

Commit it:

```bash
git add Student.txt
git commit -m "Add Rahul"
```

Then add Amit:

```text
Student Management System
Name: Rahul
Name: Amit
```

Commit it:

```bash
git add Student.txt
git commit -m "Add Amit"
```

The history looks like:

```text
main
  |
  A  Create Student file
   \
    B  Add Rahul
     \
      C  Add Amit
          |
      student-info
```

Suppose we want **only the changes from "Add Amit"** on `main`.

We can use cherry-pick.

---

## 3. Basic Cherry-Pick Command

First switch to the branch where you want the changes:

```bash
git switch main
```

Find the commit ID:

```bash
git log --oneline
```

Then:

```bash
git cherry-pick <commit_id>
```

Example:

```bash
git cherry-pick 7a82f91
```

Git applies the changes from that commit to the current branch.

The result will be:

```text
main

A---C'
 \
  B---C
      |
  student-info
```

`C'` is a **new commit** created on `main`.

The original `C` still exists on `student-info`.

---

## 4. Important Point

Cherry-pick **does not move the original commit**.

It creates a **new commit** containing the same changes.

```text
Original commit
      C
      |
      | cherry-pick
      ↓
New commit
      C'
```

Therefore:

```text
C != C'
```

They contain the same changes, but they have different commit IDs.

---

## 5. How to Find a Commit ID?

Use:

```bash
git log --oneline
```

Example:

```text
7a82f91 Add Amit
42bc921 Add Rahul
15de721 Create Student file
```

To cherry-pick `Add Amit`:

```bash
git cherry-pick 7a82f91
```

---

## 6. Cherry-Pick Multiple Commits

You can cherry-pick multiple specific commits.

```bash
git cherry-pick <commit_id1> <commit_id2>
```

Example:

```bash
git cherry-pick 42bc921 7a82f91
```

This applies both commits.

---

# 7. Cherry-Pick a Range of Commits

You can also cherry-pick a range of commits.

## Command 1: `<commit_id>..<commit_id>`

```bash
git cherry-pick <start_commit>..<end_commit>
```

### Important

The **first commit is NOT included**.

Example:

```bash
git cherry-pick A..D
```

Suppose:

```text
A---B---C---D
```

The commits picked are:

```text
B, C, D
```

So:

```text
A..D
```

means:

> Start **after A** and continue through D.

---

# 8. Include the Starting Commit Using `^`

If you want to include the starting commit too:

```bash
git cherry-pick <start_commit>^..<end_commit>
```

Example:

```bash
git cherry-pick A^..D
```

Suppose:

```text
A---B---C---D
```

The commits picked are:

```text
A, B, C, D
```

Here `A^` means:

> The **parent of commit A**.

This makes Git include `A` in the cherry-pick range.

---

## 9. Difference Between the Two Range Commands

| Command                 | Commits Picked |
| ----------------------- | -------------- |
| `git cherry-pick A..D`  | `B, C, D`      |
| `git cherry-pick A^..D` | `A, B, C, D`   |

### Easy Memory Trick

```text
A..D
```

➡️ Start **after A**

```text
A^..D
```

➡️ **Include A**

---

## 10. Cherry-Pick Conflict

Sometimes the commit being cherry-picked changes the same part of a file that has already been changed in the current branch.

Git may show a conflict:

```text
<<<<<<< HEAD
Name: Amit
=======
Name: Rahul
>>>>>>> 7a82f91
```

You must manually fix the file.

After fixing:

```bash
git add Student.txt
```

Then:

```bash
git cherry-pick --continue
```

---

## 11. Cancel a Cherry-Pick

If you don't want to continue with the cherry-pick:

```bash
git cherry-pick --abort
```

This cancels the cherry-pick operation and returns the branch to its previous state.

---

## 12. Skip a Commit

When cherry-picking multiple commits, one commit may cause a conflict or may no longer be needed.

You can skip the current commit:

```bash
git cherry-pick --skip
```

### Remember

```text
--continue → Continue
--abort    → Cancel
--skip     → Skip
```

---

# 13. Useful Commands

### See commit history

```bash
git log --oneline
```

### See current status

```bash
git status
```

### Cherry-pick one commit

```bash
git cherry-pick <commit_id>
```

### Cherry-pick multiple commits

```bash
git cherry-pick <commit_id1> <commit_id2>
```

### Cherry-pick a range

```bash
git cherry-pick <start_commit>..<end_commit>
```

### Cherry-pick a range including the first commit

```bash
git cherry-pick <start_commit>^..<end_commit>
```

### Continue after resolving conflict

```bash
git cherry-pick --continue
```

### Cancel cherry-pick

```bash
git cherry-pick --abort
```

### Skip current commit

```bash
git cherry-pick --skip
```

### See complete branch history

```bash
git log --oneline --graph --all
```

---

# 14. Real-Life Example

Imagine a project has:

```text
main
student-info
```

The `student-info` branch contains:

```text
Add Rahul
Add Amit
Add Priya
```

But the `main` branch only needs the **Add Amit** change.

Instead of merging the complete `student-info` branch, we can use:

```bash
git switch main
git cherry-pick <Add-Amit-commit-id>
```

Now only the changes from **Add Amit** are applied to `main`.

---

# 15. Cherry-Pick vs Merge vs Rebase

| Feature                   | Merge                       | Rebase                           | Cherry-Pick            |
| ------------------------- | --------------------------- | -------------------------------- | ---------------------- |
| Purpose                   | Combine branches            | Replay commits onto another base | Apply selected commits |
| Entire branch changes     | Usually yes                 | Replays branch commits           | No                     |
| Select individual commits | No                          | Not its main purpose             | Yes                    |
| Can create new commits    | Merge commit may be created | Yes                              | Yes                    |
| Changes commit history    | Usually preserves history   | Rewrites history                 | Adds new commits       |

### Simple Memory

```text
Merge       → Bring branches together
Rebase      → Replay branch commits
Cherry-pick → Select specific commits
```

---

# 16. Cherry-Pick Workflow

A common workflow is:

```bash
# 1. Go to target branch
git switch main

# 2. Find the required commit
git log --oneline

# 3. Apply the commit
git cherry-pick <commit_id>

# 4. If conflict occurs
# Fix the file

git add .

# 5. Continue
git cherry-pick --continue
```

If you want to cancel:

```bash
git cherry-pick --abort
```

---

# 17. Quick Revision

### What is cherry-pick?

`git cherry-pick` applies the changes from a **specific commit** to the current branch.

### Basic command

```bash
git cherry-pick <commit_id>
```

### Multiple commits

```bash
git cherry-pick <commit_id1> <commit_id2>
```

### Range excluding first commit

```bash
git cherry-pick <start_commit>..<end_commit>
```

### Range including first commit

```bash
git cherry-pick <start_commit>^..<end_commit>
```

### Conflict commands

```bash
git cherry-pick --continue
git cherry-pick --abort
git cherry-pick --skip
```

### Most Important Point

> ** 🍒 Cherry-pick copies the changes of selected commit(s) and creates new commit(s) on the current branch.**
