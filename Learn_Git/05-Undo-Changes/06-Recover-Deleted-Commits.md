# Recover Deleted Commits in Git

## 📖 Introduction

Accidentally deleting commits is a common mistake, especially when using commands like:

- `git reset --hard`
- `git rebase`
- `git commit --amend`
- `git branch -D`
- `git checkout`
- `git clean`

Fortunately, Git provides several recovery mechanisms that allow you to restore lost commits in most situations.

> **Important:** In many cases, deleted commits are **not immediately removed** from Git. They can often be recovered using `git reflog` or `git fsck`.

---

# How Git Stores Commits

Git stores every commit as an object inside the `.git` directory.

Even if a commit is no longer visible in `git log`, Git usually keeps it until garbage collection (`git gc`) removes unreachable objects.

```
          Git Objects

        +-------------+
        | Commit A    |
        +-------------+
               |
        +-------------+
        | Commit B    |
        +-------------+
               |
        +-------------+
        | Commit C    |
        +-------------+
               |
        +-------------+
        | Commit D    |
        +-------------+

Deleted commits often remain inside Git until
garbage collection permanently removes them.
```

---

# Common Reasons for Lost Commits

- Accidentally running:

```bash
git reset --hard
```

- Interactive rebase mistakes

```bash
git rebase -i
```

- Force push

```bash
git push --force
```

- Branch deletion

```bash
git branch -D feature
```

- Amending commits

```bash
git commit --amend
```

---

# Recovery Method 1 – Using Git Reflog (Recommended)

This is the easiest and most common recovery method.

View the reflog:

```bash
git reflog
```

Example

```
5f9d7e1 HEAD@{0}: reset: moving to HEAD~2
7b2a6d9 HEAD@{1}: commit: Added Login Feature
3d5f8c2 HEAD@{2}: commit: Updated README
```

Recover the lost commit:

```bash
git reset --hard 7b2a6d9
```

or

```bash
git reset --hard HEAD@{1}
```

---

# Recovery Method 2 – Create a Recovery Branch

Instead of immediately resetting, create a new branch.

```bash
git checkout -b recovery-branch 7b2a6d9
```

Advantages:

- Safe
- Does not modify the current branch
- Lets you inspect the recovered commit before merging

---

# Recovery Method 3 – Using Git FSCK

If the commit is missing from the reflog, Git may still know about it.

Run:

```bash
git fsck --lost-found
```

Example Output

```
dangling commit 5b7d3a2c
[Odangling commit 8e9f1d4a
```

Inspect the commit:

```bash
git show 5b7d3a2c
```

Recover it:

```bash
git checkout -b recovered-work 5b7d3a2c
```

---

# Recovery Method 4 – Recover After Branch Deletion

Suppose you accidentally delete a branch.

```bash
git branch -D feature-login
```

Use reflog:

```bash
git reflog
```

Example

```
9c4d7e1 commit: Completed Login Feature
```

Restore it:

```bash
git checkout -b feature-login 9c4d7e1
```

Branch recovered.

---

# Recovery Method 5 – Recover After Hard Reset

Current History

```
A ---- B ---- C ---- D
```

Run:

```bash
git reset --hard B
```

History becomes

```
A ---- B
```

Recover

```bash
git reflog
```

Example

```
HEAD@{1}: commit: D
```

Restore

```bash
git reset --hard HEAD@{1}
```

History

```
A ---- B ---- C ---- D
```

Recovered successfully.

---

# Recovery Method 6 – Recover After Git Rebase

Before Rebase

```
A ---- B ---- C ---- D
```

Bad rebase removes commits.

View reflog.

```bash
git reflog
```

Find the commit before the rebase.

```
HEAD@{5}
```

Recover.

```bash
git reset --hard HEAD@{5}
```

---

# Practical Example

## Step 1

Create a repository.

```bash
mkdir Git-Recovery
cd Git-Recovery
git init
```

---

## Step 2

Create commits.

```bash
echo "Version 1" > demo.txt
git add .
git commit -m "Version 1"

echo "Version 2" >> demo.txt
git add .
git commit -m "Version 2"

echo "Version 3" >> demo.txt
git add .
git commit -m "Version 3"
```

---

## Step 3

Check history.

```bash
git log --oneline
```

Output

```
Version 3
Version 2
Version 1
```

---

## Step 4

Accidentally remove commits.

```bash
git reset --hard HEAD~2
```

Now history contains only:

```
Version 1
```

---

## Step 5

Recover using reflog.

```bash
git reflog
```

Example

```
HEAD@{1}: commit: Version 3
```

---

## Step 6

Restore.

```bash
git reset --hard HEAD@{1}
```

---

## Step 7

Verify.

```bash
git log --oneline
```

Output

```
Version 3
Version 2
Version 1
```

Recovery successful.

---

# Recovery Workflow

```
        Commit History

A ---- B ---- C ---- D

        Accident

git reset --hard B

History

A ---- B

        Recovery

git reflog

↓

HEAD@{1}

↓

git reset --hard HEAD@{1}

Recovered

A ---- B ---- C ---- D
```

---

# Git Reflog vs Git FSCK

| Git Reflog | Git FSCK |
|------------|----------|
| Shows HEAD history | Finds unreachable Git objects |
| Easier to use | Advanced recovery tool |
| Best for recent mistakes | Useful if reflog is unavailable |
| Recommended first | Used as a last resort |

---

# Best Practices

✅ Commit your work frequently.

✅ Push important commits to a remote repository.

✅ Create backup branches before destructive operations.

```bash
git branch backup-before-reset
```

✅ Check the reflog before assuming work is lost.

```bash
git reflog
```

✅ Verify a recovered commit before resetting.

```bash
git show <commit-id>
```

---

# Common Mistakes

### Mistake 1

Running:

```bash
git gc
```

before attempting recovery.

Garbage collection may permanently remove unreachable commits.

---

### Mistake 2

Force pushing without understanding the impact.

```bash
git push --force
```

---

### Mistake 3

Using:

```bash
git reset --hard
```

without checking the reflog.

---

### Mistake 4

Recovering the wrong commit.

Always verify with:

```bash
git show <commit-id>
```

---

# Summary

- Deleted commits are often recoverable.
- `git reflog` is the first tool you should use.
- `git fsck --lost-found` helps find unreachable commits.
- Create a recovery branch before restoring commits.
- Avoid running `git gc` until recovery is complete.
- Regular commits and backups reduce the risk of permanent data loss.

---

# Useful Commands

```bash
git reflog
git fsck --lost-found
git show <commit-id>
git checkout -b recovery <commit-id>
git reset --hard <commit-id>
git reset --hard HEAD@{1}
git log --oneline
```

---

# Interview Questions

### What is the best way to recover deleted commits?

Use `git reflog` to find the lost commit, then restore it using `git reset --hard <commit-id>` or create a recovery branch.

---

### What is `git fsck` used for?

`git fsck` checks the integrity of the Git repository and can identify dangling or unreachable commits that may still be recoverable.

---

### Can deleted commits always be recovered?

Not always. Commits can usually be recovered until Git's garbage collection permanently removes unreachable objects.

---

### Why is creating a recovery branch recommended?

It allows you to inspect and preserve recovered commits without changing the current branch, making the recovery process safer.

---

### What should you avoid before attempting commit recovery?

Avoid running `git gc` or performing operations that permanently remove unreachable Git objects before you've tried to recover the lost commits.
