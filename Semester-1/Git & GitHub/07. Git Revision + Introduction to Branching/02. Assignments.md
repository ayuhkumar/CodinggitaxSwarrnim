
# Assignments

---

### Assignment 1: Core Commands Revision

**Objective:** Strengthen understanding of basic Git commands.

**Tasks:**
1. Write the purpose of each of the following commands in your own words:
   - `git clone`
   - `git status`
   - `git add .`
   - `git commit -m "message"`
   - `git log --oneline`
   - `git push origin main`

2. What is the difference between `git log` and `git log --oneline`?

3. Why should we write meaningful commit messages? Give 3 good and 3 bad examples.

**Submission:** Written answers

---

### Assignment 2: Two Methods to Push Code

**Objective:** Understand both ways of pushing code to GitHub.

**Tasks:**
1. Explain **Method 1** (when repository is already cloned) with the correct sequence of commands.

2. Explain **Method 2** (starting from a local folder) with the full sequence of commands.

3. Write the purpose of these commands:
   - `git init`
   - `git remote add origin <url>`
   - `git branch -M main`
   - `git push -u origin main`

4. What does the `-u` flag do in `git push -u origin main`?

**Submission:** Written answers

---

### Assignment 3: Practical – Push Using Method 2

**Objective:** Perform the complete flow of creating a local repository and pushing it to GitHub.

**Tasks:**
1. Create a new folder on your computer named `Day7_Practice`.
2. Inside it, create a file `about.txt` and write your name and one Git command you learned.
3. Perform the following commands in order:
   ```bash
   git init
   git add .
   git status
   git commit -m "Added about file"
   git log --oneline
   git remote add origin <your-github-repo-url>
   git branch -M main
   git push -u origin main
   ```
4. Verify that the file appears on GitHub.

**Submission:**  
- Screenshot of `git log --oneline`  
- Screenshot of successful push  
- Screenshot of the file on GitHub

---

### Assignment 4: Understanding Branching

**Objective:** Explain the concept of branching clearly.

**Tasks:**
1. What is a **branch** in Git? Explain in your own words.
2. Why do we need branching? Write at least 4 points.
3. What problems occur if everyone works directly on the `main` branch?
4. Explain the road analogy of branching (main road vs side road).
5. What is the default branch name in modern Git repositories?

**Submission:** Written answers.

---

### Assignment 5: Conceptual + Reflection

**Objective:** Check overall understanding of Day 7.

**Tasks:**
1. Fill in the blanks:
   - `git add` moves changes from ______ to ______.
   - `git commit` saves changes in the ______ repository.
   - `git push` uploads commits to ______.

2. Write the correct sequence of commands for Method 2 (from `git init` to `git push`).

3. Answer in 3–4 lines each:
   - When should you use Method 1?
   - When should you use Method 2?

4. Write 3 key takeaways from today.

**Submission:** Written answers
