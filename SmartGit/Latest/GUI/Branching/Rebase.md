---
redirect_from:
  - /SmartGit/Latest/Rebase
  - /SmartGit/Latest/Rebase.html
---

# Rebasing in SmartGit
In SmartGit, there are several ways to initiate a rebase:

- **Menu and toolbar:** On the Working tree window, select **Branch\|Rebase** to open the **Rebase** dialog, where you can select the branch to rebase the HEAD onto, or the branch to rebase onto the HEAD, respectively. 
You can open this dialog using the **Rebase** toolbar button, depending on your toolbar settings.
- **Branches view:** In the **Branches** view, you can right-click on a branch and select **Rebase** to rebase your current HEAD onto the selected branch.
- On the **Log Graph** of the **Log** window, you can use either of these approaches:
  - **Option 1:** You can perform a rebase by right-clicking on a commit and selecting **Rebase** from the context-menu. 
  - **Option 2:** You can drag and drop commits or refs and then select to rebase in the occurring dialog after the drop.

Just like a merge, a rebase may fail due to merge conflicts.
If that happens, SmartGit will leave the working tree in *rebasing* state, allowing you to either resolve the conflicts or to **Abort** the rebase manually.

## Rebasing ONTO

**Rebase Onto** operations can be performed from the **Log** window.

Consider the following example:  You want the `quickfix2` branch to start on the `main` branch instead of the `quickfix1` branch.

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

To achieve this, drag the `q2a` commit onto the `x (main)` commit. You will get the follwoing desired result:

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

Git rebase conflicts differ from regular merge conflicts because *left* and *right* files are swapped. When rebasing branch `A` onto branch `B`, Git first checks out branch `B`, then applies all commits from branch `A`.
If a conflict occurs, `HEAD` still points to branch `B`, and the *left* file refers to the version in branch `B`.

## Interactive Rebase

Refer to the [Interactive Rebase](Rebase-Interactive.md) section in SmartGit's documentation for more information on *interactive rebasing*.
