# Git Restore

## 📖 Introduction

`git restore` is used to restore files in your working directory or unstage files from the staging area without changing your commit history.

It is one of the safest Git commands because it only affects your local changes and does not remove commits.

---

# Why Use Git Restore?

You can use `git restore` when:

- You accidentally modified a file and want to discard the changes.
- You staged a file by mistake and want to unstage it.
- You want to restore a file to the latest committed version.
- You need to recover a file from another commit.

---

# Git Restore Workflow

```
          Modify File
               │
               ▼
      Working Directory
               │
   git restore <file>
               │
               ▼
 Restored to Last Commit

```

---

# Basic Syntax

```bash
git restore <file-name>
```

Example:

```bash
git restore app.py
```

This command discards all uncommitted changes made to **app.py**.

---

# Check File Status

Before restoring a file, check its status.

```bash
git status
```

Example Output:

```
modified: app.py
```

---

# Restore a Single File

Modify a file:

```bash
echo "Hello Git" >> app.py
```

Check status:

```bash
git status
```

Restore the file:

```bash
git restore app.py
```

Check again:

```bash
git status
```

The file is now restored to its last committed version.

---

# Restore Multiple Files

```bash
git restore file1.txt file2.txt file3.txt
```

Example:

```bash
git restore app.py config.yml README.md
```

---

# Restore All Modified Files

Restore every modified file in the current directory.

```bash
git restore .
```

> ⚠️ Warning:
> All uncommitted changes in tracked files will be lost.

---

# Unstage a File

If a file has already been added to the staging area using `git add`, you can remove it from staging.

```bash
git restore --staged app.py
```

Before:

```
Changes to be committed:
    modified: app.py
```

After:

```
Changes not staged for commit:
    modified: app.py
```

---

# Restore Both Staged and Working Directory

If you want to completely discard both staged and unstaged changes:

```bash
git restore --staged app.py
git restore app.py
```

Or:

```bash
git restore --staged --worktree app.py
```

---

# Restore a File from Another Commit

Syntax:

```bash
git restore --source=<commit-id> <file>
```

Example:

```bash
git restore --source=HEAD~1 app.py
```

This restores **app.py** from the previous commit.

---

# Restore a Deleted File

If you accidentally deleted a tracked file:

```bash
rm app.py
```

Recover it:

```bash
git restore app.py
```

---

# Practical Example

### Step 1

Create a file.

```bash
touch demo.txt
```

---

### Step 2

Add some content.

```bash
echo "Git Learning" > demo.txt
```

---

### Step 3

Commit the file.

```bash
git add .
git commit -m "Initial commit"
```

---

### Step 4

Modify the file.

```bash
echo "New Line" >> demo.txt
```

---

### Step 5

Check status.

```bash
git status
```

Output:

```
modified: demo.txt
```

---

### Step 6

Discard changes.

```bash
git restore demo.txt
```

---

### Step 7

Verify.

```bash
cat demo.txt
```

Output:

```
Git Learning
```

The added line has been removed.

---

# Git Restore vs Git Checkout

| Git Restore | Git Checkout |
|-------------|--------------|
| New Git command | Older command |
| Safer | Can perform multiple operations |
| Easier to understand | More complex |
| Used for restoring files | Used for switching branches and restoring files |

---

# Best Practices

✅ Always run:
[O
```bash
git status
```

before using `git restore`.

✅ Restore individual files whenever possible.

✅ Avoid using:

```bash
git restore .
```

unless you're certain you want to discard all changes.

✅ Commit important work before restoring files.

---

# Common Mistakes

### Mistake 1

Restoring a file without checking its contents.

Solution:

```bash
git diff
```

---

### Mistake 2

Using restore on important work.

Solution:

Commit your work first.

---

### Mistake 3

Confusing restore with reset.

- **git restore** → Restores files
- **git reset** → Moves HEAD and changes commit history

---

# Summary

- `git restore` restores files to a previous state.
- It is used to discard local changes safely.
- It can unstage files using `--staged`.
- It does not modify Git commit history.
- It is safer and easier than the older `git checkout` command for restoring files.

---

# Useful Commands

```bash
git status
git restore app.py
git restore .
git restore --staged app.py
git restore --staged --worktree app.py
git restore --source=HEAD~1 app.py
git diff
```

---

# Interview Questions

### What is git restore?

A command used to restore files in the working directory or remove files from the staging area without changing commit history.

---

### Does git restore delete commits?

No.

It only affects local file changes.

---

### Can git restore recover deleted files?

Yes, if the file was previously committed.

---

### What is the difference between git restore and git reset?

- `git restore` restores files.
- `git reset` changes the commit history and can move the HEAD pointer.

---

### When should you use git restore?

Whenever you want to discard unwanted local changes or unstage files without affecting your Git history.
