# 05. Git Commit

## What is Git Commit?

`git commit` is used to save staged changes permanently into the Git repository.

A commit acts like a **snapshot** of your project at a specific point in time. Each commit has a unique identifier (SHA hash) and becomes part of the repository history.

### Syntax

```bash
git commit -m "Commit Message"
```

Example:

```bash
git commit -m "Initial project setup"
```

---

# Why Do We Need Git Commit?

Git follows a three-step workflow:

```text
Working Directory
       |
       v
    git add
       |
       v
  Staging Area
       |
       v
   git commit
       |
       v
 Git Repository
```

Without `git commit`, changes remain only in the staging area and are not stored in Git history.

---

# Understanding a Commit

A commit contains:

* Changes made to files
* Author information
* Timestamp
* Commit message
* Unique SHA hash

Example:

```text
commit 7f3a8b2c1d4e5f67890123456789abcdef123456
Author: Newton Babu Nandru <newton@example.com>
Date: Mon Jun 22 10:30:00 2026 +0530

    Added README file
```

---

# Git Commit Workflow

```text
Create/Modify File
         |
         v
 Working Directory
         |
      git add
         |
         v
   Staging Area
         |
    git commit
         |
         v
 Repository History
```

---

# Basic Usage

## Commit Staged Changes

```bash
git commit -m "Initial commit"
```

Example Output:

```text
[main a1b2c3d] Initial commit
 1 file changed, 10 insertions(+)
 create mode 100644 README.md
```

---

# Importance of Commit Messages

Good commit messages help team members understand what changes were made.

### Bad Example

```bash
git commit -m "changes"
```

### Good Example

```bash
git commit -m "Add user authentication module"
```

### Recommended Format

```text
<Action> <Description>

Examples:

Add login page
Fix database connection issue
Update README documentation
Remove unused code
```

---

# View Commit After Creation

```bash
git log
```

Example:

```text
commit a1b2c3d
Author: Newton
Date: Mon Jun 22 10:30:00 2026

    Initial commit
```

---

# Commit All Tracked Changes

Instead of:

```bash
git add .
git commit -m "Update files"
```

Use:

```bash
git commit -am "Update files"
```

### Important

`-a` only works for:

* Modified files
* Deleted files

It does NOT include:

* New files

New files must still be added first.

---

# Amend Last Commit

Modify the most recent commit.

```bash
git commit --amend -m "Updated commit message"
```

Example:

```bash
git commit --amend -m "Initial project setup"
```

Use Cases:

* Fix typo in commit message
* Add forgotten file to last commit

---

# Commit with Editor

Without `-m`:

```bash
git commit
```

Git opens the configured editor.

Example:

```text
Add login functionality

- Created login page
- Added authentication logic
- Updated documentation
```

Save and exit to create commit.

---

# Real-World Example

## Step 1: Create Repository

```bash
mkdir commit-demo
cd commit-demo

git init
```

---

## Step 2: Create File

```bash
touch README.md
```

---

## Step 3: Check Status

```bash
git status
```

Output:

```text
Untracked files:
README.md
```

---

## Step 4: Stage File

```bash
git add README.md
```

---

## Step 5: Commit File

```bash
git commit -m "Add README file"
```

Output:

```text
[main a1b2c3d] Add README file
```

---

## Step 6: Verify Commit

```bash
git log
```

Output:

```text
commit a1b2c3d

Add README file
```

---

# Commit Lifecycle

```text
Create File
     |
     v

Untracked
     |
 git add
     |
     v

Staged
     |
 git commit
     |
     v

Committed
     |
 Modify File
     |
     v

Modified
     |
 git add
     |
     v

Staged Again
     |
 git commit
     |
     v

New Commit
```

---

# Understanding Commit Hashes

Each commit receives a unique SHA-1 hash.

Example:

```text
7f3a8b2c1d4e5f67890123456789abcdef123456
```

Short version:

```text
7f3a8b2
```

Git uses these hashes to identify commits.

Example:

```bash
git show 7f3a8b2
```

---

# Common Commit Types

### Feature

```bash
git commit -m "Add payment gateway integration"
```

### Bug Fix

```bash
git commit -m "Fix login validation issue"
```

### Documentation

```bash
git commit -m "Update installation guide"
```

### Refactoring

```bash
git commit -m "Refactor authentication service"
```

### Configuration

```bash
git commit -m "Update Docker configuration"
```

---

# Git Commit vs Git Add

| Feature                | git add | git commit |
| ---------------------- | ------- | ---------- |
| Stages Changes         | Yes     | No         |
| Creates Snapshot       | No      | Yes        |
| Updates History        | No      | Yes        |
| Required Before Commit | Yes     | N/A        |

Example:

```bash
git add app.py
```

Moves file to staging area.

```bash
git commit -m "Add app.py"
```

Stores changes permanently.

---

# Git Commit Diagram

```text
          Working Directory
                   |
                   v
              git add
                   |
                   v
             Staging Area
                   |
              git commit
                   |
                   v
           Repository History
                   |
                   v
             git log
```

---

# Hands-On Lab

## Lab 1: Create Your First Commit

### Step 1

Create repository:

```bash
mkdir commit-lab
cd commit-lab

git init
```

---

### Step 2

Create file:

```bash
touch notes.txt
```

---

### Step 3

Check status:

```bash
git status
```

---

### Step 4

Stage file:

```bash
git add notes.txt
```

---

### Step 5

Commit file:

```bash
git commit -m "Add notes file"
```

---

### Step 6

Verify commit:

```bash
git log
```

Expected Output:

```text
commit abc123

Add notes file
```

---

### Step 7

Modify file:

```bash
echo "Git Practice" >> notes.txt
```

---

### Step 8

Stage changes:

```bash
git add notes.txt
```

---

### Step 9

Create second commit:

```bash
git commit -m "Update notes"
```

---

### Step 10

View history:

```bash
git log --oneline
```

Output:

```text
f4g5h6i Update notes
a1b2c3d Add notes file
```

---

# Common Errors

## Error 1: Nothing to Commit

Command:

```bash
git commit -m "Test"
```

Output:

```text
nothing to commit, working tree clean
```

Reason:

No staged changes exist.

Solution:

```bash
git add .
git commit -m "Your message"
```

---

## Error 2: Author Identity Unknown

Output:

```text
Author identity unknown
```

Reason:

Git username/email not configured.

Solution:

```bash
git config --global user.name "Newton Babu Nandru"

git config --global user.email "newton@example.com"
```

---

## Error 3: No Staged Changes

Output:

```text
no changes added to commit
```

Solution:

```bash
git add .
git commit -m "Commit message"
```

---

# Best Practices

### Keep Commits Small

Good:

```text
Add login functionality
```

Bad:

```text
100 unrelated changes
```

---

### Write Meaningful Messages

Good:

```text
Fix API timeout issue
```

Bad:

```text
Update
```

---

### Commit Frequently

Benefits:

* Easier rollback
* Better history
* Simpler troubleshooting

---

# Common Interview Questions

## Q1. What does `git commit` do?

**Answer:**

Creates a permanent snapshot of staged changes in the repository.

---

## Q2. Is `git add` required before `git commit`?

**Answer:**

Yes.

Only staged changes are committed.

---

## Q3. What does `-m` mean?

**Answer:**

Allows adding a commit message directly from the command line.

Example:

```bash
git commit -m "Initial commit"
```

---

## Q4. What is a commit hash?

**Answer:**

A unique SHA identifier assigned to every commit.

---

## Q5. What does `git commit --amend` do?

**Answer:**

Modifies the most recent commit.

---

# Key Takeaways

✅ `git commit` saves staged changes permanently.

✅ Each commit is a snapshot of the project.

✅ Every commit has a unique SHA hash.

✅ Good commit messages improve collaboration.

✅ `git commit -m` is the most commonly used form.

✅ `git commit --amend` updates the latest commit.

---

# Quick Reference

```bash
# Commit staged changes
git commit -m "Commit message"

# Commit tracked changes
git commit -am "Commit message"

# Amend last commit
git commit --amend -m "Updated message"

# View commit history
git log

# Compact history
git log --oneline
```

