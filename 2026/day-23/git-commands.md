# Git Branching Commands

## List branches
git branch

## Create branch
git branch feature-1

## Switch branch (old way)
git checkout feature-1

## Create and switch branch
git checkout -b feature-2

## Switch branch (new way)
git switch main
git switch feature-1

## Make commit on feature branch
git add .
git add feature1.txt
git commit -m "Commit on feature branch"

## Verify branch isolation
git switch main
git log --oneline

## Delete branch
git branch -d feature-2
git branch -D feature-2

