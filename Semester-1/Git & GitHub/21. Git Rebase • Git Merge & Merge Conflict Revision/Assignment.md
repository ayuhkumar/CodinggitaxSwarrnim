Absolutely. For the practical questions, instead of giving students the branch/commit diagram directly, we can ask them to **create their own scenario** with meaningful branch and commit names.

Here is a revised assignment with more realistic scenarios.

# Assignment: Git Rebase, Git Merge & Merge Conflict

**Instructions:** Attempt all questions. Use proper Git commands and show the required commit history wherever asked.

---

## Q1. Rebase, Merge & Merge Conflict 

Answer the following:

1. Define **Git Merge**, **Merge Conflict**, and **Git Rebase**.
2. Explain **Merge vs Rebase** with a suitable diagram.
3. Write three advantages of Git Rebase.
4. Explain why Rebase is useful in real-life projects.
5. Explain the purpose of:

   * `git rebase --continue`
   * `git rebase --abort`
   * `git rebase --skip`

---

## Q2. Merge and Rebase

### Scenario: E-Commerce Website

You are working on an e-commerce project.

Create the following scenario yourself:

* Create a `main` branch.
* Create a branch named `product-page`.
* Make **two commits** on `product-page` related to the product page.
* Make **two new commits** on `main` related to other website updates.

### Tasks

1. Show the commit history using a diagram similar to:

```text
A---B---C---D  main
     \
      E---F    product-page
```

Use your **own meaningful commit messages** instead of `A, B, C...`.

2. Merge `product-page` into `main`.
3. Show the commit history after the merge (submit the screenshot).
4. Reset/recreate the scenario if required and perform a **rebase of `product-page` onto `main`**.
5. Show the commit history after the rebase(submit the screenshot).
6. Write **two differences** you observed between the merge and rebase results.

 
** Submission ** : GitHub Repo link + Screenshots + Photos of written answers

---

# Q3. Rebase Conflict

### Scenario: Student Management System

You are developing a student management system.

Create your own Git scenario using:

* `main` branch
* `student-profile` branch

### Tasks

1. Create the `student-profile` branch from `main`.
2. On `student-profile`, make **two commits** related to the student profile.
3. Switch to `main` and make a change to the **same line of the same file**.
4. Switch back to `student-profile`.
5. Rebase `student-profile` onto `main`:

```bash
git rebase main
```

6. Resolve the rebase conflict.
7. Complete the rebase using:

```bash
git add .
git rebase --continue
```

8. Create another small rebase-conflict scenario and demonstrate:

```bash
git rebase --abort
```

Explain what happened to the branch after aborting.

9. Demonstrate:

```bash
git rebase --skip
```

Explain which commit was skipped.

10. Finally, display the commit history using following command and submit the screenshot:

```bash
git log --oneline --graph --all
```

** Submission ** : GitHub Repo link + Screenshots + Photos of written answers.

---

### Deadline: 20th Sept, 2026.


