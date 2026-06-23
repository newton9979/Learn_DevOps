# 03. Git Status

## What is Git Status?

`git status` is one of the most frequently used Git commands.

It shows the current state of the repository, including:

* Current branch
* Modified files
* Staged files
* Untracked files
* Files ready to commit
* Merge conflicts (if any)

### Syntax

```bash
git status
```

---

# Why Git Status is Important?

Before performing operations like:

```bash
git add
git commit
git push
```

developers usually run:

```bash
git status
```

to understand:

* What has changed?
* Which files are staged?
* Which files are not tracked?
* What will be included in the next commit?

Think of `git status` as a **health check command** for your Git repository.

---

# How Git Tracks Files

Git categorizes files into different states.

```text
                 Git File Lifecycle

                        Create File
                              |
                              v
                     Untracked File
                              |
                        git add
                              |
                              v
                       Staged File
                              |
                       git commit
                              |
                              v
                      Tracked File
                              |
                       Modify File
                              |
                              v
                     Modified File
                              |
                        git add
                              |
                              v
                       Staged File
```

---

# Repository States

## 1. Untracked Files

Files that Git has never seen before.

Example:

```bash
touch app.py

git status
```

Output:

```text
Untracked files:
  app.py
```

Git is informing you that the file exists but is not being tracked.

---

## 2. Staged Files

Files added to the staging area using:

```bash
git add app.py
```

Check status:

```bash
git status
```

Output:

```text
Changes to be committed:
  new file: app.py
```

These changes will be included in the next commit.

---

## 3. Modified Files

After committing, if you edit a file:

```bash
vim app.py
```

Check status:

```bash
git status
```

Output:

```text
Changes not staged for commit:
  modified: app.py
```

Git knows the file changed but hasn't been staged again.

---

## 4. Committed Files

After committing:

```bash
git commit -m "Initial commit"
```

Status becomes:

```bash
git status
```

Output:

```text
nothing to commit, working tree clean
```

Repository is synchronized.

---

# Basic Usage

## Check Repository Status

```bash
git status
```

Example Output:

```text
On branch main

No commits yet

nothing to commit
```

---

# Real-World Example

## Step 1: Create Repository

```bash
mkdir git-status-demo
cd git-status-demo

git init
```

---

## Step 2: Check Status

```bash
git status
```

Output:

```text
On branch main

No commits yet

nothing to commit
```

---

## Step 3: Create File

```bash
touch README.md
```

Check status:

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

Check status:

```bash
git status
```

Output:

```text
Changes to be committed:
  new file: README.md
```

---

## Step 5: Commit File

```bash
git commit -m "Add README"
```

Check status:

```bash
git status
```

Output:

```text
nothing to commit, working tree clean
```

---

## Step 6: Modify File

```bash
echo "Git Learning" >> README.md
```

Check status:

```bash
git status
```

Output:

```text
Changes not staged for commit:
  modified: README.md
```

---

# Understanding Git Status Output

Example:

```bash
git status
```

Output:

```text
On branch main

Changes to be committed:
  modified: app.py

Changes not staged for commit:
  modified: README.md

Untracked files:
  notes.txt
```

Meaning:

| File      | State     |
| --------- | --------- |
| app.py    | Staged    |
| README.md | Modified  |
| notes.txt | Untracked |

---

# Short Status Format

Git provides a compact output.

Command:

```bash
git status --short
```

or

```bash
git status -s
```

Example:

```text
M  app.py
 M README.md
?? notes.txt
```

Meaning:

| Symbol | Meaning   |
| ------ | --------- |
| M      | Modified  |
| A      | Added     |
| D      | Deleted   |
| R      | Renamed   |
| ??     | Untracked |

---

# Status Code Explanation

```text
XY filename
```

Where:

* X = Staging Area Status
* Y = Working Directory Status

Examples:

```text
M  app.py
```

Modified and staged.

```text
 M app.py
```

Modified but not staged.

```text
A  app.py
```

Added and staged.

```text
?? app.py
```

Untracked file.

---

# Git Status Workflow Diagram

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
                    Staged
```

---

# Comparing Status States

| State     | Description                 |
| --------- | --------------------------- |
| Untracked | New file not tracked        |
| Modified  | File changed after commit   |
| Staged    | Ready for commit            |
| Committed | Saved in repository history |

---

# Common Scenarios

## Scenario 1: New File

```bash
touch app.py
git status
```

Output:

```text
Untracked files:
  app.py
```

---

## Scenario 2: Added File

```bash
git add app.py
git status
```

Output:

```text
Changes to be committed:
  new file: app.py
```

---

## Scenario 3: Modified File

```bash
echo "Hello" >> app.py

git status
```

Output:

```text
Changes not staged for commit:
  modified: app.py
```

---

## Scenario 4: Deleted File

```bash
rm app.py

git status
```

Output:

```text
deleted: app.py
```

---

# Hands-On Lab

## Lab 1: Observe File States

### Step 1

Create repository:

```bash
mkdir status-lab
cd status-lab

git init
```

### Step 2

Create file:

```bash
touch notes.txt
```

### Step 3

Check status:

```bash
git status
```

Observe:

```text
Untracked files:
notes.txt
```

### Step 4

Stage file:

```bash
git add notes.txt
```

### Step 5

Check status:

```bash
git status
```

Observe:

```text
Changes to be committed:
new file: notes.txt
```

### Step 6

Commit file:

```bash
git commit -m "Add notes"
```

### Step 7

Modify file:

```bash
echo "Git Practice" >> notes.txt
```

### Step 8

Check status:

```bash
git status
```

Observe:

```text
Changes not staged for commit:
modified: notes.txt
```

---

# Common Errors

## Error 1: Not a Git Repository

```bash
git status
```

Output:

```text
fatal: not a git repository
```

Solution:

```bash
git init
```

or move into an existing repository.

---

## Error 2: Wrong Directory

Check location:

```bash
pwd
```

Navigate to repository:

```bash
cd my-project
```

---

# Common Interview Questions

## Q1. What does `git status` do?

**Answer:**

Displays the current state of the repository including staged, modified, and untracked files.

---

## Q2. Does `git status` modify files?

**Answer:**

No.

It is a read-only command.

---

## Q3. What does `??` mean in `git status -s`?

**Answer:**

The file is untracked.

---

## Q4. What does "working tree clean" mean?

**Answer:**

There are no pending changes to commit.

---

## Q5. What is the difference between staged and modified?

| Staged           | Modified                  |
| ---------------- | ------------------------- |
| Ready for commit | Changed but not staged    |
| Stored in index  | Only in working directory |

---

# Key Takeaways

✅ `git status` displays the current state of the repository.

✅ Shows untracked, modified, and staged files.

✅ Helps verify changes before committing.

✅ Does not modify repository data.

✅ `git status -s` provides a compact output.

✅ One of the most commonly used Git commands.

---

# Quick Reference

```bash
# Show repository status
git status

# Short status
git status -s

# Alternative short form
git status --short

# Check current branch and changes
git status
```

