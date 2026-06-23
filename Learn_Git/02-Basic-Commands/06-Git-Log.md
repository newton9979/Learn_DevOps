# 06. Git Log

## What is Git Log?

`git log` is used to view the commit history of a Git repository.

It displays information about commits, including:

* Commit ID (SHA Hash)
* Author Name
* Author Email
* Date and Time
* Commit Message

### Syntax

```bash
git log
```

---

# Why Git Log is Important?

Git repositories may contain hundreds or thousands of commits.

`git log` helps developers:

* Track project history
* Identify who made changes
* Review previous work
* Investigate issues
* Find specific commits
* Audit repository activity

Think of `git log` as the **history book of your Git repository**.

---

# Understanding a Commit

Every commit has a unique SHA hash.

Example:

```text
commit a1b2c3d4e5f67890123456789abcdef12345678
Author: Newton Babu Nandru <newton@example.com>
Date:   Mon Jun 22 10:30:00 2026 +0530

    Initial project setup
```

### Components

| Field       | Description               |
| ----------- | ------------------------- |
| Commit Hash | Unique identifier         |
| Author      | Person who created commit |
| Date        | Commit timestamp          |
| Message     | Description of change     |

---

# Basic Usage

## View Complete Commit History

```bash
git log
```

Example Output:

```text
commit f7d9a8b2c1e
Author: Newton Babu Nandru <newton@example.com>
Date: Mon Jun 22 10:30:00 2026

    Added README

commit a4f6d3b8e2a
Author: Newton Babu Nandru <newton@example.com>
Date: Sun Jun 21 14:00:00 2026

    Initial commit
```

---

# Git Log Workflow

```text
Create File
     |
     v
git add
     |
     v
git commit
     |
     v
Repository History
     |
     v
git log
     |
     v
View Commits
```

---

# Common Git Log Options

## Show One-Line Output

Instead of full details:

```bash
git log --oneline
```

Example:

```text
f7d9a8b Added README
a4f6d3b Initial commit
```

Benefits:

* Easy to read
* Compact format
* Most commonly used option

---

## Limit Number of Commits

Show only recent commits.

```bash
git log -n 5
```

or

```bash
git log --max-count=5
```

Example:

```text
Last 5 commits displayed
```

---

## Show Commit Statistics

```bash
git log --stat
```

Example:

```text
commit a4f6d3b

 README.md | 10 ++++++++++
 app.py    | 20 ++++++++++++++++++++

 2 files changed, 30 insertions(+)
```

Shows:

* Files modified
* Insertions
* Deletions

---

## Show Patch (Code Changes)

```bash
git log -p
```

Displays:

* Commit details
* Exact code changes

Example:

```diff
+ print("Hello Git")
```

Useful for code reviews.

---

## Show Commit Graph

```bash
git log --graph
```

Example:

```text
* commit abc123
|
* commit xyz789
|
* commit pqr456
```

Useful for visualizing branches and merges.

---

## Pretty One-Line Graph

```bash
git log --oneline --graph --all
```

Example:

```text
* 1ab2345 Added feature
* 7cd8910 Updated README
* 9ef4567 Initial commit
```

---

# Filtering Commit History

## Commits by Author

```bash
git log --author="Newton"
```

Example:

```text
commit a1b2c3d
Author: Newton
```

---

## Search by Commit Message

```bash
git log --grep="feature"
```

Example:

```text
commit 123abc
Added new feature
```

---

## Commits Since a Date

```bash
git log --since="2026-06-01"
```

---

## Commits Until a Date

```bash
git log --until="2026-06-30"
```

---

## Commits Between Dates

```bash
git log --since="2026-06-01" --until="2026-06-30"
```

---

# Real-World Example

## Step 1: Create Repository

```bash
mkdir git-log-demo
cd git-log-demo

git init
```

---

## Step 2: Create First Commit

```bash
touch README.md

git add README.md

git commit -m "Initial commit"
```

---

## Step 3: Create Second Commit

```bash
echo "Git Tutorial" >> README.md

git add README.md

git commit -m "Updated README"
```

---

## Step 4: View History

```bash
git log
```

Output:

```text
commit 7e8f9d0
Updated README

commit 1a2b3c4
Initial commit
```

---

## Step 5: Compact History

```bash
git log --oneline
```

Output:

```text
7e8f9d0 Updated README
1a2b3c4 Initial commit
```

---

# Visual Commit History

OBOBOB```text
OBOBOB                    Commit History

Initial Commit
       |
OBOBOB       v

Updated README
       |
OBOBOBOBOBOB       v

Added app.py
       |
       v

Fixed Bug
       |
       v

Current HEAD
```

---

# Understanding HEAD

When viewing logs:

```bash
git log
```

Git starts from:

OBOBOB```text
HEAD
```

OBOBOBHEAD points to the latest commit.

Example:
OBOBOB
```text
HEAD
OBOBOB |
OBOBOB v

Commit 4
 |
Commit 3
 |
Commit 2
 |
Commit 1
```

---

OBOBOB# Git Log vs Git Status
OBOBOB
| Feature                 | git log | git status |
OBOBOBOBOBOB| ----------------------- | ------- | ---------- |
| Shows History           | Yes     | No         |
OBOBOB| Shows Current Changes   | No      | Yes        |
OBOBOB| Displays Commits        | Yes     | No         |
| Repository Health Check | No      | Yes        |
OBOBOB
Example:

```bash
git log
```

Shows past commits.

```bash
git status
```
OBOBOB
Shows current working state.

OBOBOB---
OBOBOB
# Useful Git Log Commands
OBOBOB
### Compact History

OBOBOB```bash
git log --oneline
```

### Last 3 Commits

```bash
git log -3
```

### Graph View

```bash
git log --graph
```

### Show Statistics

```bash
OBOBOBgit log --stat
OBOBOB```

OBOBOB### Show Code Changes

OBOBOB```bash
git log -p
```

### Search by Author

```bash
git log --author="Newton"
```

### Search by Message

```bash
git log --grep="bug"
```

---

# Hands-On Lab

OBOBOB## Lab 1: Explore Commit History

### Step 1
OBOBOB
OBOBOBCreate repository:

```bash
OBOBOBmkdir log-lab
OBOBOBcd log-lab

git init
```

### Step 2

Create file:

```bash
touch notes.txt
```

### Step 3

Commit:

```bash
git add notes.txt

git commit -m "Add notes"
```

### Step 4

Modify file:
OBOBOB
```bash
OBOBOBecho "Git Practice" >> notes.txt

OBOBOBgit add notes.txt

git commit -m "Update notes"
OBOBOB```

OBOBOB### Step 5

View history:

```bash
git log
```

### Step 6

View compact history:

```bash
git log --oneline
```

### Step 7

OBOBOBView graph:
OBOBOB
```bash
OBOBOBgit log --graph --oneline
```
OBOBOB
---
OBOBOB
# Common Errors

OBOBOB## Error 1: No Commits Yet

Command:

```bash
git log
```

Output:

```text
fatal: your current branch does not have any commits yet
```

Reason:

OBOBOBNo commits have been created.

OBOBOBSolution:
OBOBOB
```bash
OBOBOBgit add .

OBOBOBgit commit -m "Initial commit"
```

---

## Error 2: Not a Git Repository

Command:

```bash
git log
```
OBOBOB
Output:

OBOBOB```text
OBOBOBfatal: not a git repository
```
OBOBOB
OBOBOBSolution:

OBOBOB```bash
git init
```

or move into an existing Git repository.

---

# Common Interview Questions

## Q1. What does `git log` do?

**Answer:**

OBOBOBDisplays the commit history of a Git repository.
OBOBOB
---
OBOBOB
## Q2. How do you display commits in a single line?
OBOBOB
```bash
git log --oneline
OBOBOB```

---

## Q3. How do you view only the last 5 commits?

```bash
git log -5
```

---
OBOBOBOBOBOB
## Q4. What is a commit hash?
OBOBOB
OBOBOB**Answer:**

OBOBOBA unique SHA identifier assigned to every commit.

Example:

```text
f7d9a8b2c1e
```

---

## Q5. How do you search commits by message?

```bash
git log --grep="feature"
OBOBOB```

OBOBOB---

# Key Takeaways
OBOBOB
OBOBOB✅ `git log` displays repository commit history.

OBOBOB✅ Every commit has a unique SHA hash.
OBOBOB
✅ `git log --oneline` provides compact output.

✅ `git log --graph` visualizes branch history.

✅ Supports filtering by author, date, and message.

✅ Essential for troubleshooting and auditing changes.

---

# Quick Reference

```bash
# View complete history
git log

# Compact history
OBOBOBOBOBOBgit log --oneline
OBOBOB
OBOBOBOBOBOB# Last 5 commits
git log -5
OBOBOB
# Graph view
OBOBOBgit log --graph

OBOBOB# Show statistics
git log --stat

# Show code changes
git log -p

# Search by author
git log --author="Newton"

# Search by message
git log --grep="bug"
```

