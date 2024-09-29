# Rebasing

The git `Rebase` command allows you to apply commits from a source branch to another target branch WITHOUT creating a new merge commit, resulting in a linear commit history on the target branch.
Rebase can be viewed as more powerful version of [Cherry-Pick](Cherry-Pick.md), optimized to apply multiple commits from one branch to another.

Depending on the state of the source and target branches, rebase can use the below approaches:
- **Fast Forward** of new commits - if there are no new commits on the target branch which are not present in the source branch, and if the the target branch can simply be updated to 'point' at HEAD of the source branch without creating new commits.
- **Rewritten Commits** - if there are new commits in both source and target branches, git will need to rewrite commits in the target branch (assigning new SHA hashes).

In addition, `rebase` allows for advanced history rewriting and cleanup operations, including squashing, deleting, modifying, and reordering of existing commits.

After a successful rebase, the HEAD of the target branch will point to the new fork.

## Example

In the below, we are rebasing selected commit `E` (on the source branch) onto the `main` (target) branch.

```
git rebase a-branch main
```
 
``` text
o  [> main] A               o  [> main] A'
|                             |
o   B                         o  B'
|                             |
o   C                         o  C'
|                             |
|   o  [a-branch] D           |   o  [a-branch] D
|   |                         |  /
|   |                         | /
|   o  E (selected)   ===>    o   E
|  /                          |
| /                           |
o   F                         o   F
```

*Note: the commit history of the new `main` fork will be rewritten - although the commits C', B' and A' have the same changes as the original commits C, B and A respectively, 
 
 a new SHA hash will be assigned for each commit rewritten after the rebase is completed.
