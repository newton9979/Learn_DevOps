# 07. Git Diff

## What is Git Diff?

`git diff` is used to compare changes between files, commits, branches, or the working directory.

It shows exactly what has changed line by line, making it one of the most powerful debugging and code review tools in Git.

### Syntax

```bash
git diff
```

---

# Why Git Diff is Important?

Before committing code, developers often want to see:

* What changed?
* Which lines were modified?
* What was added?
* What was removed?
* What will be committed?

`git diff` provides these answers.

Think of it as a **change inspector** for your Git repository.

---

# Understanding Git Diff

Git compares two versions of content and displays the differences.

### Symbols Used

```diff
- Old Content
+ New Content
```

Where:

| Symbol | Meaning        |
| ------ | -------------- |
| `-`    | Removed line   |
| `+`    | Added line     |
| Space  | Unchanged line |

Example:

```diff
- print("Hello")
+ print("Hello Git")
```

---

# Git Diff Workflow

```text
              Repository
                    |
                    v
              Last Commit
                    |
                    v
            Working Directory
                    |
                git diff
                    |
                    v
             Show Changes
```

---

# Basic Usage

## Compare Working Directory with Staging Area

```bash
git diff
```

Shows changes that are:

* Modified
* Not staged

Example:

File before:

```python
print("Hello")
```

Modified file:

```python
print("Hello Git")
```

Command:

```bash
git diff
```

Output:

```diff
- print("Hello")
+ print("Hello Git")
```

---

# Compare Staged Changes

Once changes are staged:

```bash
git add app.py
```

Use:

```bash
git diff --staged
```

or

```bash
git diff --cached
```

Output:

```diff
- print("Hello")
+ print("Hello Git")
```

This shows what will be included in the next commit.

---

# Compare Specific Files

```bash
git diff app.py
```

Example:

```bash
git diff README.md
```

Displays differences only for the selected file.

---

# Compare Two Commits

Syntax:

```bash
git diff COMMIT1 COMMIT2
```

Example:

```bash
git diff a1b2c3d f4g5h6i
```

Output:

```diff
+ Added feature X
- Removed old code
```

---

# Compare Two Branches

Syntax:

```bash
git diff branch1 branch2
```

Example:

```bash
git diff main feature-login
```

Shows differences between branches.

---

# Compare Current Commit with Previous Commit

```bash
git diff HEAD~1 HEAD
```

Meaning:

```text
HEAD~1 = Previous Commit
HEAD   = Current Commit
```

---

# Compare Current Changes with Last Commit

```bash
git diff HEAD
```

Shows all current changes compared to the latest commit.

---

# Real-World Example

## Step 1: Create Repository

```bash
mkdir diff-demo
cd diff-demo

git init
```

---

## Step 2: Create File

```bash
echo "Hello" > app.py
```

Commit:

```bash
git add app.py

git commit -m "Initial commit"
```

---

## Step 3: Modify File

```bash
echo "Hello Git" > app.py
```

---

## Step 4: Check Difference

```bash
git diff
```

Output:

```diff
- Hello
+ Hello Git
```

---

## Step 5: Stage File

```bash
git add app.py
```

---

## Step 6: Compare Staged Changes

```bash
git diff --staged
```

Output:

```diff
- Hello
+ Hello Git
```

---

# Git Diff Diagram

```text
                    Repository
                          |
                          v
                     Last Commit
                          |
          -----------------------------
          |                           |
          v                           v

 Staging Area                 Working Directory
          |                           |
          |                           |
 git diff --staged            git diff
          |                           |
          v                           v

   Show Staged             Show Unstaged
     Changes                  Changes
```

---

# Git Diff Output Structure

Example:

```diff
diff --git a/app.py b/app.py
index 1234567..89abcde 100644
--- a/app.py
+++ b/app.py

-print("Hello")
+print("Hello Git")
```

### Explanation

| Line       | Meaning                  |
| ---------- | ------------------------ |
| diff --git | Comparison information   |
| index      | Internal Git identifiers |
| ---        | Old version              |
| +++        | New version              |
| -          | Removed line             |
| +          | Added line               |

---

# Useful Git Diff Commands

## Show Unstaged Changes

```bash
git diff
```

---

## Show Staged Changes

```bash
git diff --staged
```

---

## Show Changes for a File

```bash
git diff README.md
```

---

## Compare Two Commits

```bash
git diff commit1 commit2
```

---

## Compare Two Branches

```bash
git diff main feature-branch
```

---

## Compare with Last Commit

```bash
git diff HEAD
```

---

# Git Diff vs Git Status

| Feature                   | git diff   | git status |
| ------------------------- | ---------- | ---------- |
| Shows File Changes        | Yes        | No         |
| Shows Added/Removed Lines | Yes        | No         |
| Shows Repository State    | No         | Yes        |
| Shows Staged Files        | Indirectly | Yes        |

Example:

```bash
git status
```

Output:

```text
modified: app.py
```

But:

```bash
git diff
```

Shows:

```diff
- old line
+ new line
```

---

# Hands-On Lab

## Lab 1: Observe Changes

### Step 1

Create repository:

```bash
mkdir diff-lab
cd diff-lab

git init
```

### Step 2

Create file:

```bash
echo "Version 1" > notes.txt
```

### Step 3

Commit file:

```bash
git add notes.txt

git commit -m "Version 1"
```

### Step 4

Modify file:

```bash
echo "Version 2" > notes.txt
```

### Step 5

View difference:

```bash
git diff
```

Observe:

```diff
- Version 1
+ Version 2
```

### Step 6

Stage file:

```bash
git add notes.txt
```

### Step 7

View staged difference:

```bash
git diff --staged
```

---

# Common Errors

## Error 1: No Output

Command:

```bash
git diff
```

Output:

```text
(no output)
```

Reason:

There are no unstaged changes.

Verify:

```bash
git status
```

---

## Error 2: Wrong Commit ID

Command:

```bash
git diff abc xyz
```

Output:

```text
fatal: bad revision
```

Solution:

Check available commit IDs:

```bash
git log --oneline
```

---

# Git Diff Use Cases

### Code Review

```bash
git diff
```

Review changes before commit.

---

### Verify Staged Changes

```bash
git diff --staged
```

Ensure only intended changes are committed.

---

### Compare Releases

```bash
git diff release-v1 release-v2
```

Find changes between versions.

---

### Investigate Bugs

```bash
git diff commit1 commit2
```

Identify when a bug was introduced.

---

# Common Interview Questions

## Q1. What does `git diff` do?

**Answer:**

Displays line-by-line differences between versions of files.

---

## Q2. What is the difference between `git diff` and `git diff --staged`?

| Command             | Comparison                        |
| ------------------- | --------------------------------- |
| `git diff`          | Working Directory vs Staging Area |
| `git diff --staged` | Staging Area vs Repository        |

---

## Q3. How do you compare two commits?

```bash
git diff commit1 commit2
```

---

## Q4. What do `+` and `-` mean?

| Symbol | Meaning      |
| ------ | ------------ |
| `+`    | Added line   |
| `-`    | Removed line |

---

## Q5. How do you compare two branches?

```bash
git diff main feature-branch
```

---

# Key Takeaways

✅ `git diff` shows file changes line by line.

✅ Helps review modifications before committing.

✅ Supports comparison between files, commits, and branches.

✅ `git diff` shows unstaged changes.

✅ `git diff --staged` shows staged changes.

✅ Essential for debugging, code reviews, and auditing.

---

# Quick Reference

```bash
# Show unstaged changes
git diff

# Show staged changes
git diff --staged

# Compare specific file
git diff app.py

# Compare commits
git diff commit1 commit2

# Compare branches
git diff main feature-branch

# Compare with latest commit
git diff HEAD
```

