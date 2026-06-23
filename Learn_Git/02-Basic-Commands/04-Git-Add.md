# 04. Git Add

## What is Git Add?

`git add` is used to move changes from the **Working Directory** to the **Staging Area**.

Before Git can create a commit, it needs to know which files should be included. The `git add` command tells Git to start tracking new files or prepare modified files for the next commit.

### Syntax

```bash
git add <file-name>
```

Example:

```bash
git add app.py
```

---

# Why Do We Need Git Add?

Git follows a three-stage workflow:

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
 Repository
```

Without running `git add`, Git will not include changes in a commit.

---

# Understanding the Git Workflow

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
                   Git Repository
```

### Working Directory

The place where you create and modify files.

Example:

```bash
echo "Hello Git" > app.py
```

---

### Staging Area

A temporary area where Git collects changes before creating a commit.

Files enter the staging area using:

```bash
git add app.py
```

---

### Repository

The permanent history stored after a commit.

```bash
git commit -m "Initial commit"
```

---

# Basic Usage

## Add a Single File

```bash
git add app.py
```

Status before:

```bash
git status
```

Output:

```text
Untracked files:
  app.py
```

After adding:

```bash
git status
```

Output:

```text
Changes to be committed:
  new file: app.py
```

---

## Add Multiple Files

```bash
git add file1.txt file2.txt file3.txt
```

Example:

```bash
git add README.md app.py config.yaml
```

---

## Add All Files

Add all files and directories.

```bash
git add .
```

Example:

```bash
git add .
```

This stages:

* New files
* Modified files
* Deleted files

---

## Add Everything in Repository

```bash
git add -A
```

or

```bash
git add --all
```

---

# Difference Between git add . and git add -A

| Command            | Description                       |
| ------------------ | --------------------------------- |
| `git add .`        | Adds changes in current directory |
| `git add -A`       | Adds all changes in repository    |
| `git add file.txt` | Adds specific file                |

Example:

```bash
git add .
```

Stages everything under the current directory.

---

# Real-World Example

## Step 1: Create Repository

OBOBOB```bash
mkdir git-add-demo
cd git-add-demo

git init
```

---

## Step 2: Create Files
OBOBOB
```bash
OBOBOBtouch app.py

OBOBOBtouch README.md
```
OBOBOB
Check status:

```bash
git status
```

Output:

```text
Untracked files:
  README.md
  app.py
```

---

## Step 3: Add One File

```bash
git add app.py
OBOBOB```
OBOBOB
Check status:
OBOBOB
OBOBOB```bash
git status
OBOBOB```

Output:
OBOBOB
```text
Changes to be committed:
  new file: app.py

Untracked files:
  README.md
```

---

## Step 4: Add Remaining Files

```bash
git add README.md
```

Check status:

OBOBOBOBOBOB```bash
git status
OBOBOB```

OBOBOBOutput:
OBOBOB
```text
OBOBOBChanges to be committed:
  new file: README.md
  new file: app.py
```

---

# Staging Modified Files

Suppose file already exists.

Modify it:

```bash
echo "New Feature" >> app.py
```
OBOBOB
Check status:

OBOBOB```bash
git status
OBOBOB```

OBOBOBOutput:

```text
Changes not staged for commit:
  modified: app.py
```

Stage it:

```bash
git add app.py
```

Now:

```bash
git status
OBOBOB```
OBOBOB
Output:

OBOBOB```text
Changes to be committed:
OBOBOB  modified: app.py
```

---
OBOBOB
# Add Deleted Files

Delete file:

```bash
rm app.py
```

Check status:

```bash
git status
```

Output:

```text
deleted: app.py
```
OBOBOB
Stage deletion:
OBOBOB
OBOBOB```bash
OBOBOBgit add app.py
```
OBOBOB
or

```bash
OBOBOBgit add -A
```

Now Git is ready to commit the deletion.

---

# Interactive Staging

Git allows partial staging.

```bash
git add -p
```

Output:

```text
Stage this hunk [y,n,q,a,d,e,?]?
OBOBOB```

OBOBOBOBOBOBUseful when you want to commit only specific changes.
OBOBOB
---
OBOBOB
OBOBOB# Git Add Workflow Diagram

OBOBOB```text
            Create File
                  |
                  v
           Untracked File
                  |
             git add
                  |
                  v
            Staging Area
                  |
            git commit
                  |
                  v
              Repository
```

---

OBOBOB# File Lifecycle Example
OBOBOB
```text
README.md
OBOBOBOBOBOB
OBOBOBCreated
OBOBOB   |
   v
OBOBOB
Untracked
   |
git add README.md
   |
   v

Staged
   |
git commit
   |
   v

Tracked
   |
Modify File
   |
OBOBOBOBOBOB   v

OBOBOBOBOBOBModified
   |
OBOBOBgit add README.md
OBOBOB   |
   v

OBOBOBStaged Again
```

OBOBOB---

# Common Scenarios

## Scenario 1: Add One File

```bash
git add app.py
```

Stages only app.py.

---

## Scenario 2: Add Multiple Files

```bash
git add app.py README.md
OBOBOBOBOBOBOBOBOB```

Stages both files.
OBOBOB
OBOBOB---

OBOBOB## Scenario 3: Add Entire Project
OBOBOB
```bash
git add .
```

Stages all changes.

---

## Scenario 4: Stage Everything

```bash
git add -A
```

Stages:

* New files
* Modified files
* Deleted files

---

# Hands-On Lab

## Lab 1: Stage Files

### Step 1

Create repository:

```bash
mkdir add-lab
cd add-lab

git init
```

---

### Step 2

Create files:

```bash
touch app.py

touch README.md
```

---

### Step 3

Check status:

```bash
git status
```

Observe:

```text
Untracked files:
app.py
README.md
```

---

### Step 4

Stage one file:

```bash
git add app.py
```

---

### Step 5

Check status:

```bash
git status
```

Observe:

```text
Changes to be committed:
app.py

Untracked:
README.md
```

---

### Step 6

Stage all files:

```bash
git add .
```

---

### Step 7

Verify:

```bash
git status
```

Output:

```text
Changes to be committed:
app.py
README.md
```

---

# Common Errors

## Error 1: File Not Found

Command:

```bash
git add app1.py
```

Output:

```text
fatal: pathspec 'app1.py' did not match any files
```

Reason:

File does not exist.

Solution:

```bash
ls
```

Verify filename.

---

## Error 2: Not a Git Repository

Command:

```bash
git add app.py
```

Output:

```text
fatal: not a git repository
```

Solution:

```bash
git init
```

---

# Git Add vs Git Commit

| Feature                    | git add | git commit |
| -------------------------- | ------- | ---------- |
| Stages Changes             | Yes     | No         |
| Creates Commit             | No      | Yes        |
| Updates Repository History | No      | Yes        |
| Required Before Commit     | Yes     | N/A        |

Example:

```bash
git add app.py
```

Moves file to staging area.

```bash
git commit -m "Add app.py"
```

Stores change permanently in repository history.

---

# Common Interview Questions

## Q1. What does `git add` do?

**Answer:**

Moves changes from the Working Directory to the Staging Area.

---

## Q2. Is `git add` mandatory before commit?

**Answer:**

Yes.

Git commits only staged changes.

---

## Q3. What is the difference between `git add .` and `git add -A`?

**Answer:**

| Command      | Behavior                       |
| ------------ | ------------------------------ |
| `git add .`  | Adds current directory changes |
| `git add -A` | Adds all repository changes    |

---

## Q4. Can `git add` stage modified files?

**Answer:**

Yes.

It stages both new and modified files.

---

## Q5. What is the staging area?

**Answer:**

A temporary area where Git collects changes before creating a commit.

---

# Key Takeaways

✅ `git add` stages files for commit.

✅ Moves changes from Working Directory to Staging Area.

✅ Can stage single files, multiple files, or entire projects.

✅ `git add .` stages all changes in current directory.

✅ `git add -A` stages all repository changes.

✅ Required before running `git commit`.

---

# Quick Reference

```bash
# Add specific file
git add app.py

# Add multiple files
git add app.py README.md

# Add current directory changes
git add .

# Add all repository changes
git add -A

# Interactive staging
git add -p

# Verify staged changes
git status
```

