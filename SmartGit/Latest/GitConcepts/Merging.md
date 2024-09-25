# Merging

Merging branches is an essential and common operation within any Git repository, allowing for changes between two or more branches to be combined.

Examples of merging include:
- When changes made in feature branches are now complete, and are ready to be merged into a main branch such as `master`
- When fixes have been made to a previous release, and the fixes need to be merged back into a feature branch which is currently under development

## 'Normal' Merge

A common merging technique is the `merge` commit, where two or more parent commits (i.e., the last commit from the current branch and the last commit from the merged branch) are merged by creating a new 'merge' commit.
A merge commit will be created when merging with `git merge --no-ff`, or when a fast-forward merge is not possible.

In the following example, we will merge the `a-branch` into `master` (`>` indicates the HEAD pointer on the master branch):
- before the merge (left)
- after the merge (right), where a merge commit has been created to bring the changes in `a-branch` into the `master` branch:

``` text
                            o [> master]
                            |\
o [> master]                o \
|                  ==>      |  |
|  o [a-branch]             |  o [a-branch]
.  .                        .  .
```

Notes:
- When using merge commits, the full history of the feature branch is retained, and this can be visually represented by tools such as SmartGit.
- If conflicts are encountered during the merge as a result of both current and merged branches changing, then the conflicts must be resolved by using a tool like the [Conflict Solver](Conflict-Solver.md) before the merge commit can be completed.

## Fast-forward Merge

If the current branch is fully contained within the branch to be merged (i.e., the latter is simply a few commits ahead), no
additional commits are necessary. 

Unless configured otherwise, by default, git will attempt a fast forward merge where possible. 
The `--ff-only` switch will cause the merge to fail if a fast-forward merge is not possible.

Instead, the branch pointer of the current branch is moved forward to match the branch pointer of the other
branch, as shown below:

**TODO** Need to improve this diagram. Need to show the feature branch, and then the commits added linearly onto master.

``` text
o [origin/master]             o [> master][origin/master]
|                     ==>     |
o [> master]                  o
.                             .
```

Notes:
- Unlike Merge Commits, fast-forward merges create no additional commits in the repository
- Commits applied through fast-forward merges appear linearly in the target branch's history.

## Squash Merge

A squash merge works like a normal merge, except that all the new commits on the merge branch will be replaced by a single new commit representing all changes.
e.g. A squash merge helps keep the remote repository clean, as it will result in the appearance of a single commit representing changes made on a feature branch on the trunk branch.

``` text
                            o [> master] (changes from a-branch)
                            |
o [> master]                o
|                  ==>      |
|  o [a-branch]             |  o [a-branch]
.  .                        .  .
```

Note:
- Squash merges are useful for reducing commmit history 'noise' when it has taken multiple commits to complete a feature
  (e.g. bug fixes or code review feedback has resulted in multiple commits on a feature branch prior to merging into a trunk branch such as `master`)
- Squash merges may lose some historical information about who and when changes were made on the feature branch.


## Merge versus Rebase
**TODO** - Move to GitConcepts/Rebase.md?

A Git-specific alternative to merging is *rebasing* (see [Rebase](Rebase.md)), which can be used to keep the history of a branch linear.
Interactive rebasing is an advanced feature which allows any number of commits in the commit history of a branch to be modified, including:

- **picking** - including the commit in the rewritten commit history
- **squashing** - as with a squash commit, multiple commits are rewritten as one single commit
- **editing** - changing the content of a previuous commit
- **dropping** - i.e. removing a commit from the history
- **rewording** a commit message

In addition to rebasing, SmartGit provides even more advanced branch cleanup features, including:
- **splitting** a commit out into multiple commits
- easing the **reordering** of commits

Please refer to [History Cleaning Tools](GitCommands/CleanupTools.md) for details.

**TODO** check this content (was original) seems out of place.
For example, if a user has made local commits and performs a pull with merge, a merge commit with two parent commits—the user's last
and last commit from the tracked branch—is created. 
When using rebase instead of merge, Git applies the local commits on top of the commits from the tracked branch, avoiding a merge commit.
