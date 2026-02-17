1. What is a branch in Git?

A branch in Git is like a separate line of development.
It allows you to work on new features, bug fixes, or experiments without affecting the main code.

Technically, a branch is just a pointer to a commit.



2. Why do we use branches instead of committing everything to main?

We use branches because:

To keep main stable

To work on new features safely

To fix bugs without breaking production code

To allow multiple developers to work in parallel

To test changes before merging them into main

If everything is committed to main, mistakes can directly break the project.


3. What is HEAD in Git?

HEAD is a pointer that tells Git where you are currently working.

It usually points to the latest commit of the current branch

When you switch branches, HEAD moves to that branch
Example:
HEAD → main → commit-id



4. What happens to your files when you switch branches?

When you switch branches:

Git updates your working directory

Files change to match the snapshot of the target branch

Files that are different between branches will change automatically

Uncommitted changes may:

Prevent switching (conflict)

Or be carried over if Git can safely do it

Best practice: commit or stash changes before switching branches



### Difference between origin and upstream

- **origin**: Default remote pointing to your forked repository

- **upstream**: Remote pointing to the original repository you forked from



### Difference between git fetch and git pull

- `git fetch`: Downloads changes but does NOT merge them

- `git pull`: Fetches + automatically merges changes into current branch



### Difference between clone and fork

- **Clone**: Creates a local copy of a repository

- **Fork**: Creates a copy of a repository under your GitHub account



### When to clone vs fork?

- Clone → when you have direct access to the repo

- Fork → when contributing to someone else’s project


### How to keep a fork in sync with original repo?

git remote add upstream <original-repo-url>

git fetch upstream

git merge upstream/main
