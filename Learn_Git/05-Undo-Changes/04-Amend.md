# Git Commit --Amend

## 📖 Introduction

`git commit --amend` is used to **modify the most recent commit**. It allows you to:

- Change the commit message.
- Add forgotten files to the last commit.
- Remove files from the last commit.
- Correct small mistakes without creating an additional commit.

Instead of creating a new commit, Git **replaces the previous commit with a new one**.

> **Note:** Since `git commit --amend` rewrites Git history, avoid using it on commits that have already been pushed to a shared repository.

---

# Why Use Git Commit --Amend?

You can use `git commit --amend` when:

- You forgot to include a file in your last commit.
- You made a typo in the commit message.
- You need to make a small correction immediately after committing.
- You want to keep the commit history clean.

---

# How Git Commit --Amend Works

Suppose your commit history is:

```
A ---- B ---- C (HEAD)
```

After running:

```bash
git commit --amend
```

Git replaces commit **C** with a new commit.

```
A ---- B ---- C' (HEAD)
```

> **C'** is a new commit with a different commit hash.

---

# Basic Syntax

```bash
git commit --amend
```

Git opens the default editor, allowing you to update the commit message.

---

# Change Only the Commit Message

Current commit:

```
Added Login Featre
```

Oops! There is a typo.

Run:

```bash
git commit --amend
```

Update the message:

```
Added Login Feature
```

Save and close the editor.

---

# Change the Commit Message Without Opening an Editor

```bash
git commit --amend -m "Added Login Feature"
```

---

# Add Forgotten Files to the Last Commit

Suppose you forgot to include `config.yml`.

Stage the file:

```bash
git add config.yml
```

Amend the previous commit:

```bash
git commit --amend
```

Now the previous commit includes both the original changes and `config.yml`.

---

# Amend Without Changing the Commit Message

If you only want to add files:

```bash
git add .
git commit --amend --no-edit
```

`--no-edit` keeps the existing commit message unchanged.

---

# Practical Example

## Step 1

Create a file.

```bash
echo "Hello Git" > demo.txt
```
[O
---

## Step 2

Commit the file.

```bash
git add .
git commit -m "Initial Commit"
```

---

## Step 3

Forgot another file.

```bash
echo "Configuration" > config.txt
```

---

## Step 4

Stage it.

```bash
git add config.txt
```

---

## Step 5

Amend the commit.

```bash
git commit --amend
```

Result:

The previous commit now contains both files.

---

# View the Updated Commit

```bash
git log --oneline
```

Example:

Before:

```
4b3a2d1 Initial Commit
```

After amend:

```
8c7d6e5 Initial Commit
```

Notice that the commit hash changed.

---

# Git Commit --Amend Workflow

```
Before

A ---- B ---- C

Forgot a file

git add config.yml

git commit --amend

After

A ---- B ---- C'
```

The old commit is replaced by a new one.

---

# Git Commit --Amend vs New Commit

| Git Commit --Amend | New Commit |
|--------------------|------------|
| Replaces last commit | Creates another commit |
| Changes commit hash | New hash for new commit |
| Keeps history clean | Adds another history entry |
| Best for small corrections | Best for new work |

---

# Git Commit --Amend vs Git Reset

| Git Commit --Amend | Git Reset |
|--------------------|-----------|
| Modifies last commit | Moves HEAD |
| Keeps changes together | Can remove commits |
| Used for corrections | Used for undoing commits |

---

# Best Practices

✅ Use `git commit --amend` immediately after making the last commit.

✅ Verify the staged files before amending.

```bash
git status
```

✅ Review the updated commit.

```bash
git log --oneline
```

✅ Use `--no-edit` if you only want to add files.

---

# Common Mistakes

### Mistake 1

Amending a commit that has already been pushed.

This rewrites history and may cause issues for collaborators.

---

### Mistake 2

Forgetting to stage new files.

Always run:

```bash
git add <file>
```

before amending.

---

### Mistake 3

Changing the commit message unintentionally.

Use:

```bash
git commit --amend --no-edit
```

when only adding files.

---

# Important Note About Remote Repositories

If the amended commit has already been pushed:

```bash
git push
```

will fail because the commit history has changed.

You would need:

```bash
git push --force
```

or

```bash
git push --force-with-lease
```

> ⚠️ **Warning:** Force pushing can overwrite remote history. Use it only when you fully understand the impact and have coordinated with your team.

---

# Summary

- `git commit --amend` modifies the most recent commit.
- It can update the commit message or include forgotten files.
- It replaces the previous commit with a new one.
- The commit hash changes after amending.
- Avoid amending commits that have already been pushed to a shared repository.

---

# Useful Commands

```bash
git commit --amend
git commit --amend -m "New commit message"
git commit --amend --no-edit
git add .
git status
git log --oneline
```

---

# Interview Questions

### What is `git commit --amend`?

It modifies the most recent commit by updating its message or contents.

---

### Does `git commit --amend` create a new commit?

No. It replaces the previous commit with a new version, which receives a new commit hash.

---

### When should you use `git commit --amend`?

Use it to fix the latest commit before sharing it with others.

---

### Why should you avoid amending pushed commits?

Because it rewrites Git history and may cause conflicts for collaborators.

---

### What does `--no-edit` do?

It keeps the existing commit message while updating the contents of the last commit.
