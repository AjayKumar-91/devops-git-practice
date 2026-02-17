# Day 22 – Understanding Git Workflow

## 1. Difference between git add and git commit
git add is used to move changes from the working directory to the staging area.
git commit is used to permanently save those staged changes into the Git repository.

In simple words:
- git add = select changes
- git commit = save selected changes

---

## 2. What does the staging area do? Why not commit directly?
The staging area acts as a middle layer where we decide exactly what should go into the next commit.

Git does not commit directly because:
- We may want to commit only specific files
- We can review changes before committing
- It helps create clean and meaningful commits

---

## 3. What information does git log show?
git log shows the commit history of the repository, including:
- Commit ID (hash)
- Author name and email
- Date and time of commit
- Commit message

It helps us understand what changes were made and when.

---

## 4. What is the .git/ folder and what happens if you delete it?
The .git/ folder is the core of the Git repository.
It stores:
- Commit history
- Branch information
- Configuration
- All tracked file data

If the .git/ folder is deleted:
- The project is no longer a Git repository
- All commit history is lost
- Git commands will stop working

---

## 5. Difference between working directory, staging area, and repository

Working Directory:
- Where we create and modify files
- Changes are not tracked yet

Staging Area:
- Temporary area where changes are prepared for commit
- Files are added using git add

Repository:
- Where committed changes are permanently stored
- Managed using git commit

