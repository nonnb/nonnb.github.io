---
redirect_from:
  - /SmartGit/Latest/Branches
  - /SmartGit/Latest/Branches.html
---
# Branches

Branches are used by Git to store an independent series of commits within a repository.

In Git, you can create as many Branches in a repository as needed. For example, it is common to create branches when fixing bugs in a previous release of a software project, while simultaneously developing new features for the next project version.

Git distinguishes between two kinds of branches: 
- *Local branches*: These are branches in your local repository. If you have not pushed this branch to a remote repository, it will only be visible on your local computer.
- *Remote branches*: These are branches stored on the remote repository. These branches will be visible to everyone with access to the remote repository and will become available in your local repository when you Clone a remote repository.
You cannot work directly on remote branches; instead, you will need to clone the remote repository to work on the branch.

## Cloning, Tracking, and Local Branches
When you use `git clone` to [Clone](Clone.md) a remote repository, all remote branches will become known to the local repository as 'remote-tracking' branches.

Remote-tracking branches will have the name of the remote prepended, e.g., `origin/main`.

When you checkout from a remote-tracking branch (e.g., `git checkout origin/main -b main`), Git links the local branch to the remote-tracking branch (known as the 'upstream' for the local branch). This ensures that when you `push`, Git will know to push the commits to the original remote branch (unless you specify otherwise), and when you `pull`, Git will know which remote branch to monitor for new commits.

You can also choose to create a local branch that does not track a remote branch (e.g., `git checkout -b mybranch`). In this case, you will need to specify the source branch when merging remote changes into your local branch and provide a target remote branch when pushing.

After Cloning, Git will check out the default local branch into your Working Tree -  usually *main* (or *master* in older repositories).

## Working with Branches
Once you've cloned a repository to your local system, the `checkout` command is used to switch between branches, or create new branches in Git.

For existing local branches, checkout will simply switch the Working Tree to the branch selected, e.g.:

`git checkout ExistingFeature`

When creating new branches, unless you specify a starting point, Git assumes your new branch should be created from the current branch (referred to as `HEAD`):

`git checkout -b NewFeature` 

To create a new local branch from an existing remote branch, you'll need to specify the remote-tracking branch as the starting point, e.g.:

`git checkout -b NewFeature origin/main`

This will create a local branch `NewFeature` that tracks the upstream `origin/main`. _(Note: In some teams, development etiquette requires that you `reserve` the new branch name on the remote before checking it out locally)_.

In addition to checking out existing remote branches, Git also allows you to create new local branches from an existing commit hash, or tag, e.g.:

`git checkout -b NewFeature ce1067054f`

Where `ce1067054f` is the SHA hash of the commit that you would like the `NewFeature` local branch to be created from.
#### Tip
>
> After a creating a new release, tagging the commit that produced that release with an identifier is good practice.
This makes it easier to identify where to branch from when creating bug-fix commits for that release.
>

When you push changes from your local branch to the origin repository,
these changes will be propagated to the tracked (remote) branch as well.
Similarly, when you pull changes from the origin repository, they will also be stored in the tracked (remote) branch of the local
repository. To get the tracked branch changes into your local branch,
the remote changes must be *merged from the tracked branch*. This can
be done either directly when invoking the *Pull* command in SmartGit or
later by explicitly invoking the *Merge* command. An alternative to the
Merge command is the Rebase command.


#### Tip
>
>The method to be used by Pull (either *Merge* or *Rebase*) can be configured in **Repository\|Settings** on the **Pull** tab.
>

## Branches are just pointers to commits

Every branch is simply a pointer to a commit with a 'friendly' name that you provide (`main`, `feature-2`, etc.). A special, unique pointer in every repository is the *HEAD*, which points to the commit corresponding to the working tree's current state. *HEAD* can point to a commit or a local branch.

When working on a branch, when you stage and commit changes, a  new commit is created, which will `remember` the previous (parent) commit, from which it was based. 

In the below, we've added a new commit `B` based off commit `A`, on branch `main`. After the changes in `B` are committed:
- A is the parent commit of B
- B becomes the new commit pointer for branch `main`
- The `HEAD` pointer will move to `B`

```
o B
|
o A
```

Some other examples of commit and branch 'pointer' operations:

You can create a new branch from a previous commit by providing the commit hash (`A`) and the new branch name (`NewBranch`), e.g.:

`git checkout A -b NewBranch`

You can also checkout a previous commit WITHOUT creating a new branch by providing the commit hash (`A`) that you wish to switch to:

`git checkout A`

In this case, since no branch has been specified, git refers to the Working Tree status as a **detached HEAD**.

Although we generally recommend that you make changes when working on a named branch, if you accidentally make changes to files while in detached HEAD status which you wish to keep, you can simply create a new branch from the current HEAD status:

`git checkout -b NewBranch`

And then stage and commit the changes you've made to the `NewBranch` branch.

You can then use tools such as [Merge](Merging.md), cherry-pick, or [Rebase](Rebasing.md) to absorb these changes into another branch.
