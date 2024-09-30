---
redirect_from:
  - /SmartGit/Latest/Working-Tree-States
  - /SmartGit/Latest/Working-Tree-States.html
---
# Working Tree States

In general, the git Working Tree will be in a clean status, and you will be able to issue standard git commands such as checking out different branches, staging changes, and creating new commits.

However, there are certain situations where commits cannot be completed, such as when a merge or rebase fails due to a conflict, or during an interactive rebase.
This will leave git in an intermediate state where additional manual intervention is required (e.g. requiring you to resolve any merge conflicts, or to provide information or perform modification activities during an interactive rebase).

## Merge Conflicts (Merging status)

When a [Merge](Merge.md) or [Rebase](Rebase.md) fails due to changes in files which cannot automatically be resolved by git, git will add merge conflict markers to the conflicted files and leave the Working Tree in a Merging status.

In this case, there are two ways to complete the merge: 
- By resolving the conflict, e.g. using a tool such as the [SmartGit Conflict Resolver](/SmartGit/Latest/GUI/GitCommands/Branching/Conflict-Solver.md), staging the file changes, and committing on the working tree root.
- By reverting the entire working tree to its state prior to the attempt to merge (`git merge --abort`) or prior to the rebase (`git rebase --abort`)

SmartGit automatically detects when the Working Tree is in Merging status and will guide you through the conflict resolution process.

## Interactive Rebasing (Rebase status)

During an interactive rebase, git will require additional user input in order to complete the rebase. Examples are:
- Selecting which operation to perform with each commit (e.g. Pick, Squash, Fix, Drop etc)
- Git will pause the rebase operation if you choose to Edit one or more commits, or if you wish to edit one or more commit messages.
- Once you're done with amending a commit during an 'Edit' operation during a rebase, you'll need to prompt git to continue with the rebase.

SmartGit automatically detects when the Working Tree is in Rebase status and will guide you through the interactive rebase process.
