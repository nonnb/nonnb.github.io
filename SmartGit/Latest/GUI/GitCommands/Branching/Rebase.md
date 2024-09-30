---
redirect_from:
  - /SmartGit/Latest/Rebase
  - /SmartGit/Latest/Rebase.html
---

# Rebasing in SmartGit
In SmartGit, there are several ways to initiate a rebase:

-   **Menu and toolbar:** On the Working tree window, select **Branch\|Rebase** to open the **Rebase** dialog, where you can select the branch to rebase the HEAD onto, or the branch to rebase onto the HEAD, respectively.
    Depending on your toolbar settings, you can also open this dialog using the **Rebase* toolbar button.
-   **Branches view:** In the **Branches** view, you can right-click on a branch and select **Rebase** to rebase your current HEAD onto the selected branch.
-   On the **Log Graph** of the **Log** window, you can use either of these approaches:
  -  **Option 1:** You can perform a rebase by right-clicking on a commit and selecting **Rebase** from the context-menu. 
  -  **Option 2:** You can drag and drop commits or refs and then select to rebase in the occurring dialog after the drop.

Just like a merge, a rebase may fail due to merge conflicts.
If that happens, SmartGit will leave the working tree in *rebasing* state, allowing you to either manually resolve the conflicts or to **Abort** the rebase.

## Rebasing ONTO

**Rebase Onto** operations can be performed from the **Log** window.

Consider following example where the `quickfix2` branch should not start at the `quickfix1` branch, but rather on the `main` branch:

**TODO** the below diagram is linear, so suggest either show `main`, `quickfix1` and `quickfix2` as actual branches, or refer to `quickfix1` as a tag or commit.

``` text
      q2b (quickfix2)
      |
      q2a
    /
    q1b (quickfix1)
    |
   q1a
 /
 x (main)
 |
...
```

To achieve this, drag the `q2a` commit onto the `x (main)` commit and you will get the desired result:

``` text
q2b (quickfix2)
 |
q2a
 |
 |  q1b (quickfix1)
 |   |
 |  q1b
 | /
 x (main)
 |
...
```



## Resolving Conflicts

Git rebase conflicts are different to other kinds of merge conflicts, because *left* and *right* files are swapped: when rebasing branch `A` to `B`, Git will first checkout `B`, then applies all commits from `A`.
If a conflict occurs, `HEAD` still points to `B` and hence the *left* file would be the file as it's present in `B`.

## Interactive Rebase

For details on *interactive rebase* refer to [Interactive Rebase](Rebase-Interactive.md).
