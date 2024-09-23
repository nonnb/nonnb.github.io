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
-  If you choose **Merge to Working Tree**, SmartGit will perform the merge but leave the working tree in a *merging*
state so you can manually resolve merge conflicts and review changes. 
See the section on [Resolving Conflicts](#resolving-conflicts) for further information.

### Squash Merge

A squash merge works like a normal merge, except that replaces all new commits on the branch with a single new commit representing all changes. 
A squash merge helps merge changes from local (feature) branches when you don't want all of your feature branch commits pushed into the remote repository (e.g., multiple commits may have been made during bug fixes or code review feedback).

**Note:** Squash merges may lose some historical information about who and when changes were made on the feature branch.

``` text
                            o [> master] (changes from a-branch)
                            |
o [> master]                o
|                  ==>      |
|  o [a-branch]             |  o [a-branch]
.  .                        .  .
```

On the **Commit** dialog, you can choose between a normal merge (merge
commit) and a squash merge (simple commit). To perform a squash
merge, select **Merge to Working Tree** when initiating the
merge; otherwise, you won't see the **Commit** dialog.

### Merge versus Rebase

A Git-specific alternative to merging is *rebasing* (see
[Rebase](Rebase.md)), which can be used to keep the history linear.
For example, if a user has made local commits and performs a pull with merge, 
a merge commit with two parent commits—the user's last and last commit from the tracked branch—is created. 
When using rebase instead of merge, Git applies the local commits on top of the
commits from the tracked branch, avoiding a merge commit.

## Resolving Conflicts

When a merge, [cherry-pick](Cherry-Pick.md), [revert](Revert.md) or [rebase](Rebase.md) command fails due to
conflicting changes, SmartGit stops the operation and leaves the working tree conflicted. 
This allows you to either abort the command, resolve the conflicts, or continue the operation.
The following options are available in SmartGit:

-   **Resolve dialog:** Select a file containing conflicts and 
    invoke **Local** **\|Resolve** from SmartGit's main window menu.
    You can set the file's contents to either of the two
    conflicting versions (i.e., \`Ours' or \`Theirs'). Optionally, you may choose not to stage the resolution, meaning the conflict marker on the file won't be removed.
-   **Conflict Solver:** Select a file containing conflicts and
    invoke **Query** **\|Conflict Solver** which opens a three-way diff tool for viewing changes between the conflicting versions.
    See [Conflict Solver](Conflict-Solver.md) for details on resolving conflicts using this tool.
-   **Discard command:** To abort the merge, cherry-pick, revert or
    rebase, select the repository in the **Repositories** view and
    invoke **Branch \|Abort** or **Local** **\|Discard**.

After resolving all conflicts, you can continue with the merge, cherry-pick, or rebase by selecting the repository in the 
**Repositories** view and invoking **Local** **\|Commit**. If you are rebasing, the Commit toolbar button will have changed to
**Continue**.
