# Merging

Merging branches is an essential and common operation within any Git repository, allowing changes in two or more branches to be combined.

**Examples of merging include:**
- When changes made in feature branches are complete and ready to be merged into a main branch, such as `master`.
- When fixes have been made to a previous release and need to be merged back into a feature branch currently under development.

SmartGit supports all Git merge types. Please refer to [Merging in SmartGit for further information](/SmartGit/Latest/Merge) for further details.

## 'Normal' Merge Commit

A common merging technique is the **`merge`** commit, where two or more parent commits (i.e., the last commit from the current branch and the last commit from the merged branch) are combined by creating a new 'merge' commit.
A merge commit is created when merging with `git merge --no-ff` or when a fast-forward merge is not possible.

In the following example, we will merge the `a-branch` into `main` (`>` indicates the HEAD pointer on the main branch):
- **Before the merge (left)**
- **After the merge (right)**, where a merge commit has been created to bring the changes in `a-branch` into the `main` branch:

``` text
                            o [> master]
                            |\
o [> master]                o \
|                  ==>      |  |
|  o [a-branch]             |  o [a-branch]
.  .                        .  .
```

**Notes:**
- When using merge commits, the full history of the feature branch is retained, which can be visually represented by tools such as SmartGit.
- If conflicts arise during the merge due to the changing current and merged branches, these conflicts must be resolved using a tool such as the [SmartGit Conflict Solver](../GUI/GitCommands/Branching/Conflict-Solver.md) before the merge commit can be completed.

## Fast-forward Merge

If the current branch is fully contained within the branch to be merged (i.e., the latter is simply a few commits ahead), no
additional commits are necessary, and a `fast-forward` merge can be performed. 

Unless configured otherwise, Git will attempt a fast forward merge by default when possible. 
A fast-forward merge can be forced with the `--ff-only` switch; however, the merge will fail if a fast-forward merge is not possible (e.g., if both the current and merge branches contain new commits).

After a successful fast-forward merge, the branch pointer of the current branch is moved forward to match the branch pointer of the merge
branch, as shown below:

**TODO** Need to improve this diagram. Need to show the feature branch, and then the commits added linearly onto main.

``` text
o [origin/master]             o [> master][origin/master]
|                     ==>     |
o [> master]                  o
.                             .
```

**Notes:**
- Unlike Merge Commits, fast-forward merges create no additional commits in the repository
- Commits applied through fast-forward merges appear linearly in the target branch's history.

## Squash Merge

A **squash merge** works like a normal merge, except that all the new commits on the merge branch are combined into a single new commit representing all changes.
A squash merge helps to keep a remote repository clean by producing a single commit representing all the changes made on a feature branch, which is then merged into the trunk branch.

``` text
                            o [> master] (changes from a-branch)
                            |
o [> master]                o
|                  ==>      |
|  o [a-branch]             |  o [a-branch]
.  .                        .  .
```

**Note:**
- Squash merges help reduce commmit history 'noise' when multiple commits are made to complete a feature
  (e.g., bug fixes or code review feedback has resulted in multiple commits on a feature branch before merging into a trunk branch such as `master`).
- Squash merges may lose historical information about who made specific changes and when those changes were made on the feature branch.


## Merge versus Rebase

A Git-specific alternative to merging is **rebasing** (see *[Rebase](Rebase.md)*), which can be used to keep a branch's histor linear.
Interactive rebasing is an advanced feature that allows any number of commits in a branch's commit history to be modified, including:

- **Picking:** Including the commit in the rewritten commit history.
- **Squashing:** As with a squash commit, multiple commits are rewritten as one single commit.
- **Editing:** Changing the content of a previous commit.
- **Dropping:** Removing a commit from the history.
- **Rewording:** Modifying a commit message.

In addition to rebasing, SmartGit offers advanced branch cleanup features, such as:
- **Splitting** a commit into multiple commits.
- **Reordering** commits easily.

Please refer to [SmartGits Interactive Rebase features](../GUI/GitCommands/Branching/Rebase-Interactive.md) for more details.

**Example**

If a user has added new commits on a local branch which tracks a remote repository branch which subsequently also has new commits, the user can either perform:
- a **pull with merge**, which will create a merge commit with **two parent** commits:
  1. The user's last commit on the local branch.
  2. The last commit from the remote tracked branch.
- OR, if using **rebase** instead of merge, Git applies the local commits on top of the commits from the tracked branch, avoiding a merge commit. A new commit will represent the user's changes on the local branch.
