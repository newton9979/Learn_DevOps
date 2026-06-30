# 🏷️ Git Tags

## 📖 Introduction

Git Tags are references that point to a specific commit in a Git repository. Unlike branches, which continue to move as new commits are added, tags remain fixed to the commit where they were created.

Tags are commonly used to mark important milestones such as software releases, stable versions, or production deployments.

For example:

- v1.0.0 → Initial Release
- v1.1.0 → New Features Added
- v2.0.0 → Major Release

Git Tags make it easy to identify and revisit important points in your project's history.

---

# 🎯 Learning Objectives

After completing this topic, you will understand:

- What Git Tags are
- Why Git Tags are important
- Types of Git Tags
- How to create, view, push, and delete tags
- Semantic Versioning
- Real-world release workflow
- Best practices
- Common mistakes

---

# 🤔 Why Do We Need Git Tags?

Imagine your application has gone through multiple releases.

```
Commit A → Commit B → Commit C → Commit D → Commit E
```

You release Version 1.0 after Commit C.

Several months later, a customer reports an issue in Version 1.0.

Without a tag, finding the exact release commit can be difficult.

With Git Tags:

```
Commit A → Commit B → Commit C (v1.0.0) → Commit D → Commit E (v2.0.0)
```

You can instantly switch back to the exact version that was released.

---

# 🏷️ What is a Git Tag?

A Git Tag is a permanent pointer to a specific commit.

Unlike a branch:

- Branches continue moving as new commits are added.
- Tags never move unless deleted and recreated.

Tags are ideal for:

- Software releases
- Production deployments
- Stable versions
- Milestones

---

# 📊 Git Tags Workflow

The following diagram shows how tags mark important commits in a project's history.

![Git Tags Workflow](assets/git-tags-overview.png)

Example:

```
A ----- B ----- C ----- D ----- E
               │             │
            v1.0.0        v2.0.0
```

---

# 🏷️ Types of Git Tags

Git supports two types of tags.

## 1️⃣ Lightweight Tag

A lightweight tag is simply a pointer to a commit.

It contains:

- Tag name
- Commit reference

It does **not** contain:

- Author information
- Date
- Message
- GPG signature

Create a lightweight tag:

```bash
git tag v1.0.0
```

---

## 2️⃣ Annotated Tag

Annotated tags are recommended for software releases.

They contain:

- Tag name
- Author
- Email
- Date
- Tag message
- Optional GPG signature

Create an annotated tag:

```bash
git tag -a v1.0.0 -m "First Stable Release"
```

---

# 📊 Lightweight vs Annotated Tags

![Lightweight vs Annotated Tags](assets/lightweight-vs-annotated-tags.png)

| Feature | Lightweight | Annotated |
|----------|-------------|-----------|
| Metadata | ❌ | ✅ |
| Author | ❌ | ✅ |
| Date | ❌ | ✅ |
| Message | ❌ | ✅ |
| GPG Signature | ❌ | ✅ |
| Recommended for Releases | ❌ | ✅ |

---

# 🛠️ Common Git Tag Commands

## List All Tags

```bash
git tag
```

Example Output

```
v1.0.0
v1.1.0
v2.0.0
```

---

## Create a Lightweight Tag

```bash
git tag v1.0.0
```

---

## Create an Annotated Tag

```bash
git tag -a v1.0.0 -m "Production Release"
```

---

## View Tag Details

```bash
git show v1.0.0
```

---

## Tag a Previous Commit

```bash
git tag -a v1.0.0 4d5a2b7
```

Where `4d5a2b7` is the commit ID.

---

## Push a Single Tag

```bash
git push origin v1.0.0
```

---

## Push All Tags

```bash
git push origin --tags
```

---

## Delete Local Tag

```bash
git tag -d v1.0.0
```

---

## Delete Remote Tag

```bash
git push origin --delete v1.0.0
```

---

## Checkout a Tag

```bash
git checkout v1.0.0
```

> **Note:** This places Git in a **detached HEAD** state. Create a new branch if you plan to make changes.

```bash
git checkout -b hotfix-v1.0.0 v1.0.0
```

---

# 📦 Semantic Versioning

Git tags often follow Semantic Versioning (SemVer):

```
MAJOR.MINOR.PATCH
```

Examples:

| Version | Meaning |
|----------|----------|
| v1.0.0 | First stable release |
| v1.1.0 | New features added |
| v1.1.1 | Bug fixes |
| v2.0.0 | Major changes or breaking updates |

---

# 🚀 Release Workflow

The following diagram illustrates a typical software release process using Git Tags.

![Git Release Workflow](assets/git-release-workflow.png)

```
Development
      │
      ▼
Testing
      │
      ▼
Merge to Main
      │
      ▼
Create Tag
      │
      ▼
Push Tag
      │
      ▼
GitHub Release
      │
      ▼
Production Deployment
```

---

# 💻 Hands-on Example

Check repository status:

```bash
git status
```

Create an annotated tag:

```bash
git tag -a v1.0.0 -m "Version 1.0 Release"
```

Verify the tag:

```bash
git tag
```

Push the tag:

```bash
git push origin v1.0.0
```

View details:

```bash
git show v1.0.0
```

---

# 🌍 Real-World Use Cases

### Software Releases

Every production release is tagged.

Example:

```
v1.0.0
v1.1.0
v2.0.0
```

---

### Rollback

If the latest deployment fails:

```bash
git checkout v1.0.0
```

You can quickly return to the previous stable version.

---

### CI/CD Pipelines

Many CI/CD tools trigger deployments when a new tag is pushed.

Example:

```bash
git push origin v2.0.0
```

This can automatically initiate a production deployment.

---

# ✅ Best Practices

- Use **annotated tags** for releases.
- Follow Semantic Versioning.
- Write meaningful tag messages.
- Push tags after creating them.
- Keep tag names consistent.

Examples:

```
v1.0.0
v1.2.0
v2.0.0
```

---

# ❌ Common Mistakes

### Forgetting to Push Tags

Creating a tag locally does **not** send it to the remote repository.

Always run:

```bash
git push origin --tags
```

---

### Using Lightweight Tags for Releases

Prefer annotated tags for official releases because they include metadata.

---

### Editing Tagged Commits

Avoid changing commits after creating release tags, as it can create confusion and inconsistencies.

---

# 📌 Command Summary

| Command | Description |
|----------|-------------|
| `git tag` | List all tags |
| `git tag v1.0.0` | Create a lightweight tag |
| `git tag -a v1.0.0 -m "Release"` | Create an annotated tag |
| `git show v1.0.0` | Display tag details |
| `git push origin v1.0.0` | Push a specific tag |
| `git push origin --tags` | Push all tags |
| `git tag -d v1.0.0` | Delete a local tag |
| `git push origin --delete v1.0.0` | Delete a remote tag |
| `git checkout v1.0.0` | Checkout a tag |

---

# 🎤 Interview Questions

### 1. What is a Git Tag?

A Git Tag is a permanent reference to a specific commit, commonly used to mark software releases and important milestones.

---

### 2. What is the difference between a branch and a tag?

- A **branch** moves forward as new commits are added.
- A **tag** always points to the same commit unless it is deleted and recreated.

---

### 3. What are the two types of Git Tags?

- Lightweight Tags
- Annotated Tags

---

### 4. Why are annotated tags recommended for releases?

Annotated tags include metadata such as the author, date, message, and optional GPG signature, making them more suitable for official releases.

---

### 5. How do you push all tags to a remote repository?

```bash
git push origin --tags
```

---

### 6. What happens when you checkout a tag?

Git enters a **detached HEAD** state because the tag points directly to a commit instead of a branch.

---

# 📝 Summary

Git Tags provide a reliable way to mark important commits such as software releases and production deployments. By using annotated tags and following Semantic Versioning, teams can easily identify stable versions, simplify release management, and improve collaboration. Mastering Git Tags is an essential skill for developers, DevOps engineers, and production support professionals.
