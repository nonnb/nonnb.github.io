---
redirect_from:
  - /SmartGit/Latest/Merge
  - /SmartGit/Latest/Merge.html
---

# Merge

### 'Normal' Merge

In case of a normal merge, a merge commit with at least two parent
commits (i.e., the last commit from the current branch and the last commit from the
merged branch) is created. See the following figure, where `>` HEAD pointer indicates
a merge commit to bring changes in `a-branch` into the `master` branch:



``` text
                            o [> master]
                            |\
o [> master]                o \
|                  ==>      |  |
|  o [a-branch]             |  o [a-branch]
.  .                        .  .
```



### Fast-forward Merge

If the current branch is fully contained within the branch to be merged
(i.e., the latter is simply a few commits ahead), no
additional commits are necessary. Instead, the branch pointer of the
current branch is moved forward to match the branch pointer of the other
branch, as shown below:



``` text
o [origin/master]             o [> master][origin/master]
|                     ==>     |
o [> master]                  o
.                             .
```



### Merge in SmartGit

In SmartGit, there are several ways to initiate a merge:

-   **Menu and toolbar:** In the Working Tree window, select **Branch\|Merge** to open the **Merge** dialog, where you can choose the
    branch to be merged into the current branch. Depending on your
    toolbar settings, you can also open this dialog via the **Merge**
    button on the toolbar.
-   **Branches view:** In the **Branches** view (available in both the
    Working tree and the Log window), you can right-click on a branch and
    select **Merge** to merge the selected branch into the current
    branch.
-   **Log Graph:** In the Log graph of the **Log** window, right-click on a commit (usually the one where
    the branch to be merged points to) and selecting **Merge** from
    the context-menu.

Regardless of how you invoke the Merge command, you will be given a
choice between **Create Merge-Commit**, **Merge to Working Tree**,
and, if possible, **Fast-Forward**.

-  If you choose **Create Merge-Commit**, SmartGit will perform the merge
and create a merge commit, assuming no merge conflicts exist.
-  If there are merge conflicts, or if you choose **Merge to Working Tree**,
SmartGit will perform the merge, but leave the working tree in a
*merging* state, so that you can manually resolve merge conflicts and
review the changes to be made. See [Resolving Conflicts](#resolving-conflicts) for further information on how to deal
with merge conflicts.

### Squash Merge

A squash merge works like a normal merge, except that replaces all new commits on a branch with a single new commit representing ALL changes. 
A squash merge is useful for merging changes from local (feature) branches where you don't want all of your feature branch commits to be pushed into the remote repository (e.g. it may have taken several commits before all bugs had been resolved and code review feedback may have resulted in further commits to the feature branch).

Note : Squash merges may lose some historic information about who, and when, committed changes were made on the feature branch.

``` text
                            o [> master] (changes from a-branch)
                            |
o [> master]                o
|                  ==>      |
|  o [a-branch]             |  o [a-branch]
.  .                        .  .
```

On the **Commit** dialog, you can choose between a normal merge (merge
commit) and a squash merge (simple commit). Thus, to perform a squash
merge you have to choose **Merge to Working Tree** when initiating the
merge, as otherwise you won't see the **Commit** dialog.

### Merge versus Rebase

A Git-specific alternative to merging is *rebasing* (see
[Rebase](Rebase.md)), which can be used to keep the history linear.
For example, if a user has made local commits and performs a pull with
merge, a merge commit with two parent commits - the user's last commit
and the last commit from the tracked branch - is created. When using
rebase instead of merge, Git applies the local commits on top of the
commits from the tracked branch, thus avoiding a merge commit.

## Resolving Conflicts

When a merge, [cherry-pick](Cherry-Pick.md), [revert](Revert.md) or [rebase](Rebase.md) command fails due to
conflicting changes, SmartGit stops the operation and leaves the working
tree in a conflicted state, so that you can either abort the command,
or resolve the conflicts and continue with the command. This section
explains how you can do that with SmartGit. Generally, the following
options are available:

-   **Resolve dialog** If you select a file containing conflicts and
    then invoke **Local** **\|Resolve** in the menu of SmartGit's main
    window, you can set the file's contents to either of the two
    conflicting versions, i.e. \`Ours' or \`Theirs'. Optionally, you may
    also choose not to stage the resetting of the file contents, meaning
    that the conflict marker on that file won't be removed.
-   **Conflict Solver** Selecting a file containing conflicts and
    invoking **Query** **\|Conflict Solver** will open the configured Conflict Solver, a three-way diff tool allowing you to view the changes between the two conflicting versions. Please see [Conflict Solver](Conflict-Solver.md) for details on resolving conflicts with the SmartGit Conflict Solver.
-   **Discard command** To abort the merge, cherry-pick, revert or
    rebase, select the repository in the **Repositories** view and
    invoke **Branch \|Abort** or **Local** **\|Discard**.

Lastly, if all conflicts have been resolved, you can continue with the
merge, cherry-pick or rebase by selecting the repository in the
**Repositories** view and invoking **Local** **\|Commit**. If you are
rebasing, the Commit toolbar button has changed its name to
**Continue**.
