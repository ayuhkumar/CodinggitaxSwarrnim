
# Git Cherry-Pick — Assignment

## Instructions

* Complete all questions.
* Use meaningful branch names and commit messages.
* Perform the practical tasks using Git.
* Use `git log --oneline --graph --all` to show your commit history.
* Take screenshots of important steps if required.
* Write the answers of the theoretical questions in your notebook and submit the photos in your CodingGita_assignment repository.
* Take the screenshots of commit history of all branches and submit the screenshots + GitHub Repo link for all practical questions in your CodingGita_assignment repository.

---

# Q1. Theory — Understanding Cherry-Pick

Answer the following questions:

1. What is `git cherry-pick`?
2. What is the difference between **cherry-pick** and **merge**?
3. Does cherry-pick move the original commit? Explain.
4. Why does cherry-pick create a new commit?
5. What is the purpose of the following commands?

   * `git cherry-pick --continue`
   * `git cherry-pick --abort`
   * `git cherry-pick --skip`
6. What is the difference between:

   ```bash
   git cherry-pick <start_commit>..<end_commit>
   ```

   and

   ```bash
   git cherry-pick <start_commit>^..<end_commit>
   ```

---

# Q2. Practical — Cherry-Pick a Specific Commit

## Scenario

You are developing a **Student Management System**.

Create a new Git repository and create a file:

```text
Student.txt
```

Add:

```text
Student Management System
```

Commit it with a meaningful commit message.

### Tasks

1. Initialize the Git repository.
2. Create and commit `Student.txt`.
3. Create a new branch for student information.
4. Add information about **Rahul** and commit it.
5. Add information about **Amit** and commit it.
6. Switch back to `main`.
7. Find the commit ID of the **Amit** commit.
8. Cherry-pick only the **Amit** commit into `main`.
9. Display the commit history using:

```bash
git log --oneline --graph --all
```

### Expected Concept

The final history should show a **new cherry-picked commit on `main`**, while the original commit remains on the student-information branch.

---

# Q3. Practical — Cherry-Pick Multiple Commits

Create your own project scenario.

Examples:

* E-commerce website
* Library Management System
* Hospital Management System
* College Management System
* Food Delivery Application

### Tasks

1. Create a Git repository.
2. Create a `main` branch with an initial commit.
3. Create a meaningful feature branch.
4. Make at least **3 commits** on the feature branch.
5. Switch back to `main`.
6. Cherry-pick **any two specific commits** from the feature branch.

Use:

```bash
git cherry-pick <commit_id1> <commit_id2>
```

7. Display the history:

```bash
git log --oneline --graph --all
```

### Requirement

Do **not** use generic commit messages such as:

```text
commit 1
commit 2
commit 3
```

Use meaningful messages such as:

```text
Add product search
Add product details
Fix product price
```

---

# Q4. Practical — Cherry-Pick Commit Range

Create a repository with at least **4 commits**:

```text
A → B → C → D
```

Use meaningful commit messages instead of A, B, C, and D.

For example:

```text
Create homepage
Add navigation bar
Add login page
Fix login validation
```

### Task 1 — Excluding Starting Commit

Cherry-pick a range using:

```bash
git cherry-pick <start_commit>..<end_commit>
```

Identify which commits are selected.

---

### Task 2 — Including Starting Commit

Now use:

```bash
git cherry-pick <start_commit>^..<end_commit>
```

Identify which commits are selected.

### Answer

Explain the difference between:

```bash
git cherry-pick <start_commit>..<end_commit>
```

and:

```bash
git cherry-pick <start_commit>^..<end_commit>
```

---

# Q5. Practical — Resolve a Cherry-Pick Conflict

Create a simple project with two branches:

```text
main
feature
```

### Tasks

1. Create a file called:

```text
Student.txt
```

2. Add a student name on the `feature` branch.
3. Commit the change.
4. Switch to `main`.
5. Modify the **same line** in `Student.txt`.
6. Commit the change.
7. Try to cherry-pick the commit from `feature`.

Example:

```bash
git cherry-pick <feature_commit_id>
```

8. Resolve the conflict manually.
9. Stage the resolved file:

```bash
git add Student.txt
```

10. Continue the cherry-pick:

```bash
git cherry-pick --continue
```

11. Check the final history:

```bash
git log --oneline --graph --all
```

---

# Q6. Short Practical Questions

Perform the following commands and explain what each one does:

### 1. Find commit history

```bash
git log --oneline
```

### 2. Cherry-pick one commit

```bash
git cherry-pick <commit_id>
```

### 3. Cherry-pick multiple commits

```bash
git cherry-pick <commit_id1> <commit_id2>
```

### 4. Cherry-pick a range

```bash
git cherry-pick <start_commit>..<end_commit>
```

### 5. Cherry-pick a range including the starting commit

```bash
git cherry-pick <start_commit>^..<end_commit>
```

### 6. Continue after resolving a conflict

```bash
git cherry-pick --continue
```

### 7. Cancel cherry-pick

```bash
git cherry-pick --abort
```

### 8. Skip the current commit

```bash
git cherry-pick --skip
```

---

# Submission Checklist

Before submitting, make sure you have:

* [ ] Created your own Git repository.
* [ ] Created meaningful branches.
* [ ] Created meaningful commit messages.
* [ ] Cherry-picked a single commit.
* [ ] Cherry-picked multiple commits.
* [ ] Used a commit range.
* [ ] Used `<start_commit>^..<end_commit>`.
* [ ] Resolved a cherry-pick conflict.
* [ ] Used `--continue`.
* [ ] Used `--abort`.
* [ ] Used `--skip`.
* [ ] Checked history using:

  ```bash
  git log --oneline --graph --all
  ```
**Submission Guidelines:** Given in the instructions.
---

# Quick Revision

| Task                         | Command                           |
| ---------------------------- | --------------------------------- |
| Cherry-pick one commit       | `git cherry-pick <commit_id>`     |
| Cherry-pick multiple commits | `git cherry-pick <id1> <id2>`     |
| Range excluding start        | `git cherry-pick <start>..<end>`  |
| Range including start        | `git cherry-pick <start>^..<end>` |
| Continue                     | `git cherry-pick --continue`      |
| Cancel                       | `git cherry-pick --abort`         |
| Skip                         | `git cherry-pick --skip`          |
| View history                 | `git log --oneline --graph --all` |

> **Remember:** Cherry-pick selects specific commit changes and applies them to the current branch. It does not merge the entire branch.
