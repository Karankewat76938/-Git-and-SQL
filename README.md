# -Git-and-SQL
Here we learn about Git and SQL part 1

session 1
 — DBMS & Normalization
1. What is DBMS?

DBMS = Database Management System.

It is software that stores and manages data (e.g., MySQL, PostgreSQL, SQL Server).

Relational Database stores data in tables (rows and columns) and uses SQL to query data.

2. Logical structure and Normalization

Logical structure: how data is organized (tables, columns, keys, relationships).

Normalization: process of organizing database to reduce redundancy (duplicate data) and improve data integrity.

3. Normal Forms (NF) — simple explanations
1NF (First Normal Form)

Rule: Each table cell must contain only one value (atomicity). No repeating groups or arrays inside one cell.

Every row must be unique — usually by having a Primary Key.

No duplicate rows or repeated columns.

Example: Instead of Hobbies column with "reading, music", use separate rows or a separate table listing hobbies.

2NF (Second Normal Form)

Precondition: Table must already be in 1NF.

Rule: No partial dependency — every non-key column must depend on the whole primary key, not just part of it.

This matters for tables with composite keys (primary key made of more than one column).

If a non-key column depends only on part of the composite key, move it to another table.

Example: If primary key is (OrderID, ProductID) but ProductName depends only on ProductID, then ProductName should be in a separate Product table.

3NF (Third Normal Form)

Precondition: Table must be in 2NF.

Rule: No transitive dependency — non-key columns must depend only on the primary key, not on other non-key columns.

If A -> B and B -> C, then C should not be stored in the same table if it depends on B (a non-key). Move C to another table.

Example: If you have Employee table with EmployeeID (PK), DeptID, and DeptName, DeptName depends on DeptID (non-key), so DeptName should be in Department table.

4. ER Diagram (Entity-Relationship Diagram)

Purpose: Visual map of database tables (entities), attributes (columns), and relationships between tables.

Entities: represent tables (e.g., Customer, Order, Product).

Attributes: columns for each entity (e.g., CustomerName, Contact).

Relationships: one-to-one, one-to-many, many-to-many (use junction table for many-to-many).

Primary Key (PK) uniquely identifies each row.

Foreign Key (FK) connects tables by referencing another table’s PK.

Steps to create ER Diagram:

Identify entities from the problem domain.

List attributes for each entity and mark primary keys.

Determine relationships and their cardinality (1:1, 1:M, M:N).

Convert M:N relationships into junction tables.

Normalize to 1NF/2NF/3NF as needed.

Part B — Version Control Systems (VCS) & Git
1. What is VCS?

VCS (Version Control System) helps track changes to files (code, docs) over time.

It allows multiple people to work together, see history, revert changes, and merge work.

2. Types of VCS

Localized (local): stores revisions locally on one machine (rarely used).

Centralized: single central server (e.g., SVN); clients check out files from server.

Distributed: every developer has a full copy of the repository (history + code) — e.g., Git. This allows offline work and easier branching/merging.

# Git Session - 1
3. Why Git?

Git is an open-source, distributed VCS.

Developers can commit locally, create branches, merge, and push to a remote (GitHub, GitLab, Bitbucket).

4. Common Git Commands — explained step by step
Setup & configuration

git config --global user.name "Your Name"

Sets your Git username (displayed in commits).

git config --global user.email "you@example.com"

Sets your email for commits.

(Optional) git config --list

Shows all your config settings.

Create / Initialize repo

git init

Initializes a new local Git repository in the current folder. Creates a .git directory.

After git init, you can add files and make commits.

git clone <repository-url>

Copies a remote repository to your local machine (creates a working directory with full history).

Check status & see changes

git status

Shows changed files, staged files (ready to commit), and untracked files.

git diff

Shows line-by-line differences for files not yet staged.

git diff --staged (or git diff --cached)

Shows differences between staged files and the last commit.

Add and commit

git add <filename>

Stages a file for commit (adds changes to the index). Example: git add index.html.

git add .

Stages all changed files in current directory (be careful — it includes all modified files).

git commit -m "commit message"

Records a snapshot of staged files to the local repo with a message describing the change.

git commit -a -m "message"

Shortcut: stage (only modified tracked files) and commit in one step (doesn’t add new untracked files).

View log & history

git log

Shows commit history (author, date, commit id, message).

git log --oneline --graph --all

Compact graphical view of commit history (nice for branches).

Working with remote repositories

git remote add origin <url>

Adds a remote named origin that points to a remote repository URL.

git push origin main

Pushes your local main branch to the remote named origin.

If remote branch doesn’t exist, use git push -u origin main to set upstream.

git pull origin main

Fetches remote changes and merges them into your current branch.

git fetch

Downloads objects and refs from remote but does not merge. Useful to inspect remote changes before integrating.

Branching & merging

git branch

Lists local branches. git branch <name> creates a new branch.

git checkout <branch>

Switches to <branch>. (Older command; new alternative is git switch.)

git checkout -b <branch>

Create and switch to new branch in one step.

git merge <branch>

Merge <branch> into your current branch.

Undo / restore / remove

git restore <file>

Restore working tree file from HEAD (discard local changes to that file).

git restore --staged <file>

Unstage a file (remove it from the index), but leave working directory changes.

git reset --hard HEAD

WARNING: Discards local changes and resets to last commit. Use with caution.

git revert <commit>

Creates a new commit that undoes changes from the specified commit (safe for shared history).

Other useful commands

git show <commit>

Shows details about a specific commit.

git stash

Temporarily saves changes in a stack so you can work on something else, then git stash pop to reapply.

git rm <file>

Remove file from working tree and index (staged for deletion).

git tag <tagname>

Create a tag on current commit (useful for releases).

5. Typical Git Workflow (step-by-step)

git clone <url> (if starting from remote) or git init (if starting locally).

git checkout -b feature/my-feature — create a feature branch.

Make changes to files locally.

git status — check what changed.

git add <file> or git add . — stage changes.

git commit -m "Short message about changes" — commit locally.

git pull origin main — update your branch with latest remote changes (resolve conflicts if any).

git push origin feature/my-feature — push branch to remote.

Create a Pull Request (PR) on GitHub/GitLab to merge branch to main.

After PR approved, git merge or use platform UI to merge.

git checkout main then git pull and git branch -d feature/my-feature to delete local branch.

