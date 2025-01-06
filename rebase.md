# Git Interactive Rebase

In this README file, we will practice and understand how to use the **interactive rebase** feature of Git. This guide is structured with step-by-step instructions and examples.

---

## Prerequisites

1. Git installed on your system. [Install Git](https://git-scm.com/)
2. A basic understanding of Git commands.
3. A local Git repository with multiple commits to test on.

---

## Why Interactive Rebase?

Interactive rebase allows you to:

- Reorder commitsss
- Squash multiple commits into one
- Edit commit messages
- Remove unnecessary commits
- Split commits into smaller chunks

---

## Steps to Use Interactive Rebase

1. **Set up a repository for practice**  
   If you don’t already have a repository, create one for testing:

   ```bash
   git init interactive-rebase-demo
   cd interactive-rebase-demo
   echo "Initial file content" > file.txt
   git add file.txt
   git commit -m "Initial commit"
   ```

Add more commits:

```bash
echo "Added feature A" >> file.txt
git add file.txt
git commit -m "Added feature A"

echo "Added feature B" >> file.txt
git add file.txt
git commit -m "Added feature B"
```

2. **Start Interactive Rebase**
To rebase the last N commits interactively, run:

```bash
git rebase -i HEAD~3
```
3. **Understand the Rebase Editor**\
The editor will show a list of the last `N` commits in this format:

```bash
pick <commit-hash> Initial commit
pick <commit-hash> Added feature A
pick <commit-hash> Added feature B
```
**Available commands:**

- `pick`: Keep the commit as is.
- `reword`: Edit the commit message.
- `edit`: Amend the commit (e.g., add/remove changes).
- `squash`: Combine this commit with the previous one.
- `fixup`: Like squash but discards the commit message.
- `drop`: Remove the commit.

4. **Example Scenarios**

- Reorder Commits\
Swap the order of "Added feature A" and "Added feature B":

```bash
pick <commit-hash> Initial commit
pick <commit-hash> Added feature B
pick <commit-hash> Added feature A
```
- Squash Commits\
Combine "Added feature A" and "Added feature B":
```bash
pick <commit-hash> Initial commit
pick <commit-hash> Added feature A
squash <commit-hash> Added feature B
```

After saving, Git will prompt you to edit the combined commit message.

- Edit a Commit Message\
Change the message for "Added feature A":

```bash
pick <commit-hash> Initial commit
reword <commit-hash> Added feature A
pick <commit-hash> Added feature B
```
After saving, Git will open an editor for the new message.

5. **Finalize the Rebase**\
After making changes, save and close the editor. Git will apply the changes. If conflicts arise, resolve them manually, then continue:

```bash
git rebase --continue
```
To abort the rebase and return to the original state:

```bash
git rebase --abort
```
---
## Common Issues and Solutions
1. **Conflict Resolution**\
If a conflict occurs during rebase, Git will pause the process and show the conflicting files. Resolve conflicts, then continue the rebase:

```bash

git add <file>
git rebase --continue
```
2. **Forgot to Save Changes?**\
If you forgot to save your changes while editing a commit, you can amend it:

```bash
git commit --amend
git rebase --continue
```
3. **Stuck During Rebase?**\
To safely stop and undo the rebase:

```bash
git rebase --abort
```
---