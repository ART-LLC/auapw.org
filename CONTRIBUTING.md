# Contributing to AUAPW

Thanks for your interest in contributing to **AUAPW** (All Used Auto Parts Warehouse)! This document covers how to set up the project locally and, most importantly, the Git branching workflow we use for all changes.

## Table of Contents

- [Getting Started](#getting-started)
- [Git Branching Workflow](#git-branching-workflow)
  - [`git branch` — List, create, and delete branches](#git-branch--list-create-and-delete-branches)
  - [`git checkout` — Switch branches or restore files](#git-checkout--switch-branches-or-restore-files)
  - [`git merge` — Combine branch histories](#git-merge--combine-branch-histories)
  - [`git rebase` — Replay commits onto a new base](#git-rebase--replay-commits-onto-a-new-base)
- [Recommended Workflow](#recommended-workflow)
- [Commit Message Guidelines](#commit-message-guidelines)
- [Submitting a Pull Request](#submitting-a-pull-request)

## Getting Started

```bash
# Clone the repo
git clone https://github.com/ART-LLC/auapw.git
cd auapw

# Install dependencies
npm ci

# Start the dev server
npm run dev
```

## Git Branching Workflow

All work should happen on a feature branch, never directly on `main`. Below is a reference for the core commands you'll use.

### `git branch` — List, create, and delete branches

```bash
# List all local branches (current branch marked with *)
git branch

# List all branches, including remote-tracking branches
git branch -a

# Create a new branch (does NOT switch to it)
git branch feature/login-page

# Rename the current branch
git branch -m feature/login-page-v2

# Delete a branch (safe — refuses if unmerged)
git branch -d feature/login-page

# Force-delete a branch (even if unmerged)
git branch -D feature/login-page
```

### `git checkout` — Switch branches or restore files

```bash
# Switch to an existing branch
git checkout main

# Create a new branch AND switch to it in one step
git checkout -b feature/cart-store

# Switch to a remote branch (creates a local tracking branch)
git checkout -b feature/wishlist origin/feature/wishlist

# Discard local changes to a file (restore from the last commit)
git checkout -- lib/data.ts
```

> **Note:** Modern Git (2.23+) splits this into `git switch` (for branches) and `git restore` (for files). Either approach is fine in this project — `checkout` still works for both.

### `git merge` — Combine branch histories

```bash
# Switch to the branch you want to merge INTO (usually main)
git checkout main

# Merge a feature branch into main
git merge feature/cart-store

# Merge without fast-forward (always creates a merge commit, preserving history)
git merge --no-ff feature/cart-store

# Abort a merge if conflicts get messy
git merge --abort
```

### `git rebase` — Replay commits onto a new base

```bash
# Rebase the current branch onto the latest main (keeps history linear)
git checkout feature/cart-store
git rebase main

# Interactive rebase to squash/edit/reorder the last 3 commits
git rebase -i HEAD~3

# Continue after resolving a conflict during rebase
git rebase --continue

# Abort a rebase and return to the original state
git rebase --abort
```

**When to use which:**

| Situation | Recommended command |
|---|---|
| Bringing a shared/public branch up to date | `merge` |
| Cleaning up your own feature branch before opening a PR | `rebase` |
| Branch other people are also committing to | `merge` (avoid rebasing) |
| Want a clean, linear history for review | `rebase -i` to squash noisy commits |

## Recommended Workflow

```bash
# 1. Sync main
git checkout main
git pull origin main

# 2. Create a feature branch
git checkout -b feature/short-description

# 3. Make changes, then stage and commit
git add .
git commit -m "feat: short description of change"

# 4. Keep your branch up to date with main
git fetch origin
git rebase origin/main

# 5. Push your branch
git push origin feature/short-description

# 6. Open a pull request into main
```

## Commit Message Guidelines

We follow a lightweight [Conventional Commits](https://www.conventionalcommits.org/) style:

- `feat: ...` — a new feature
- `fix: ...` — a bug fix
- `docs: ...` — documentation only changes
- `refactor: ...` — code change that neither fixes a bug nor adds a feature
- `chore: ...` — tooling, config, or maintenance changes

## Submitting a Pull Request

1. Ensure your branch is rebased on the latest `main` and there are no conflicts.
2. Run `npm run lint` and `npm run build` locally to confirm everything passes.
3. Open a PR with a clear title and description of what changed and why.
4. Link any related issues in the PR description (e.g., `Closes #123`).
5. Request review and address feedback via additional commits (avoid force-pushing over reviewed commits when possible).

Thank you for contributing! 🚗
