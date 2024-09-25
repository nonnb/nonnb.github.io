# Rebasing

The git Rebase command allows you to apply commits from one branch to another.
Rebase can be viewed as more powerful version of [Cherry-Pick](Cherry-Pick.md), which is optimized to apply multiple commits from one branch to another.

**Rebase** "moves"* the commits below the HEAD to the selected commit. The HEAD will be moved to the new fork

e.g., in the below, we have rebased selected commit `E` is rebased onto the `master` branch.
 
 *Note: the commit history of the new fork will be rewritten - although the commits C', B' and A' have the same changes as the original commits C, B and A respectively, 
 a new SHA hash will be assigned for each commit rewritten after the rebase is completed.

``` text
o  [> master] A               o  [> master] A'
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
To **Rebase Onto** you may use the **Log** window.
Consider following example where the `quickfix2` branch should not start at the `quickfix1` branch, but rather on the `master` branch:

``` text
q2b (quickfix2)
 |
q2a
 |
q1b (quickfix1)
 |
q1a
 |
 x (master)
 |
...
```
To achieve this, just drag the `q2a` commit onto the `x (master)` commit and you will get the desired result:
``` text
q2b (quickfix2)
 |
q2a
 |
 |  q1b (quickfix1)
 |   |
 |  q1b
 | /
 x (master)
 |
...
```
