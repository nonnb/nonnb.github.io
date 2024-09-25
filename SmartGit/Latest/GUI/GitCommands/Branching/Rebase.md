# Rebasing in SmartGit
In SmartGit, there are several places from which you can initiate a rebase:

-   **Menu and toolbar** On the Working tree window, select **Branch\|Rebase** to open the **Rebase** dialog, where you can select the branch to rebase the HEAD onto, or the branch to rebase onto the HEAD, respectively.
    Depending on your toolbar settings, you can also open this dialog using the **Rebase* toolbar button.
-   **Branches view** In the **Branches** view, you can right-click on a branch and select **Rebase** to rebase your current HEAD onto the selected branch.
-   **Log Graph** On the Log graph of the **Log** window, you can perform a rebase by right-clicking on a commit and selecting **Rebase** from the context-menu.
-   **Log Graph** In the Log graph of the **Log** window, you can drag and drop commits or refs and then select to rebase in the occurring dialog after the drop.

Just like a merge, a rebase may fail due to merge conflicts.
If that happens, SmartGit will leave the working tree in *rebasing* state, allowing you to either manually resolve the conflicts or to **Abort** the rebase.

## Resolving Conflicts

Git rebase conflicts are different to other kinds of merge conflicts, because *left* and *right* files are swapped: when rebasing branch `A` to `B`, Git will first checkout `B`, then applies all commits from `A`.
If a conflict occurs, `HEAD` still points to `B` and hence the *left* file would be the file as it's present in `B`.

## Interactive Rebase

For details on *interactive rebase* refer to [Interactive Rebase](Rebase-Interactive.md).
