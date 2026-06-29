# Git Revert

## 📖 Introduction

`git revert` is used to **undo the changes introduced by a specific commit** by creating a **new commit** that reverses those changes.

Unlike `git reset`, `git revert` **does not remove or rewrite commit history**. Instead, it preserves the project history, making it the safest option for undoing changes in shared repositories.

> **Note:** `git revert` is recommended for public or shared branches because it maintains a complete and accurate commit history.

---

# Why Use Git Revert?

You can use `git revert` when:

- You want to undo a specific commit.
- The commit has already been pushed to a remote repository.
- You are working with a team and want to preserve Git history.
- You need an audit trail of all changes.

---

# How Git Revert Works

Suppose your commit history is:

```
A ---- B ---- C ---- D (HEAD)
```

If commit **D** contains a bug:

```bash
git revert HEAD
```

Git creates a new commit that reverses the changes made in **D**.

```
A ---- B ---- C ---- D ---- E (HEAD)
                    ↑
             E reverses D
```

Notice that commit **D** still exists in the history.

---

# Basic Syntax

```bash
git revert <commit-id>
```

Example:

```bash
git revert a1b2c3d
```

Git opens your default text editor for the commit message.

Default message:

```
Revert "Added login feature"
```

Save and close the editor to complete the revert.

---

# Revert the Latest Commit

Undo the most recent commit:

```bash
git revert HEAD
```

---

# Revert a Specific Commit

View commit history:

```bash
git log --oneline
```

Example:

```
7f8e9d0 Added Login Page
5c6d7e8 Updated README
3a4b5c6 Initial Commit
```

Revert the login page commit:

```bash
git revert 7f8e9d0
```

A new commit is created to undo its changes.

---

# Revert Multiple Commits

Revert several commits one by one:

```bash
git revert HEAD~2
git revert HEAD~1
git revert HEAD
```

Or revert a range without committing each one immediately:

```bash
git revert --no-commit HEAD~2..HEAD
git commit -m "Reverted last three commits"
```

---

# Practical Example

## Step 1

Create a file.

```bash
echo "Version 1" > demo.txt
```

Commit it.

```bash
git add .
git commit -m "Version 1"
```

---

## Step 2

Modify the file.

```bash
echo "Version 2" >> demo.txt
```

Commit again.

```bash
git add .
git commit -m "Version 2"
```

---

## Step 3

Check history.

```bash
git log --oneline
```

Output:

```
b2c3d4e Version 2
a1b2c3d Version 1
```

---

## Step 4

Undo the latest commit.

```bash
git revert HEAD
```

Git creates:

```
c3d4e5f Revert "Version 2"
```

---

## Step 5

View history again.

```bash
git log --oneline
```

Output:

```
c3d4e5f Revert "Version 2"
b2c3d4e Version 2
a1b2c3d Version 1
```

Notice that the original commit is still present.

---

# Git Revert Workflow

```
Original History

A ---- B ---- C ---- D

git revert D

Updated History

A ---- B ---- C ---- D ---- Revert(D)
```

History is preserved.

---

# Git Revert vs Git Reset

| Git Revert | Git Reset |
|------------|-----------|
| Creates a new commit | Moves HEAD |
| Preserves commit history | Rewrites history |
| Safe for shared branches | Best for local branches |
| Can be pushed safely | Can create conflicts after push |

---

# Git Revert vs Git Restore

| Git Revert | Git Restore |
|------------|-------------|
| Works on commits | Works on files |
| Creates a new commit | No new commit |
| Preserves history | Does not affect history |
| Used to undo committed changes | Used to discard local changes |

---

# Best Practices

✅ Use `git revert` for commits that have already been pushed.

✅ Review the commit before reverting.

```bash
git show <commit-id>
```

✅ Use meaningful commit messages if you modify the default revert message.

✅ Test your application after reverting.

---

# Common Mistakes

### Mistake 1

Using `git reset` instead of `git revert` on a shared branch.

---

### Mistake 2

Reverting the wrong commit.

Always verify the commit ID first.

```bash
git log --oneline
```

---

### Mistake 3

Ignoring merge conflicts during a revert.

Resolve conflicts, then continue:

```bash
git add .
git revert --continue
```

---

### Mistake 4

Cancelling a revert incorrectly.

If you decide not to continue:

```bash
git revert --abort
```

---

# Summary

- `git revert` undoes committed changes safely.
- It creates a new commit instead of deleting history.
- It is the recommended way to undo changes in shared repositories.
- It keeps the project history clean and traceable.
- It is safer than `git reset` when working with teams.

---

# Useful Commands

```bash
git revert HEAD
git revert <commit-id>
git revert --no-commit HEAD~2..HEAD
git revert --continue
git revert --abort
git log --oneline
git show <commit-id>
```

---

# Interview Questions

### What is git revert?

`git revert` creates a new commit that reverses the changes introduced by an earlier commit while preserving Git history.

---

### Does git revert delete commits?

No.

It creates a new commit that undoes the selected commit.

---

### When should you use git revert?

When you need to undo changes that have already been committed and shared with others.

---

### Why is git revert safer than git reset?

Because it preserves commit history and does not rewrite commits, making it safe for collaborative projects.

---

### What happens after running `git revert HEAD`?

Git creates a new commit that reverses the changes made in the latest commit while keeping the original commit in the history.
