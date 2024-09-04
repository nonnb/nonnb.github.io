# Branches

Branches are used by Git to store an independent series of commits in a repository.

In Git, you can create as many Branches in a repository as needed, e.g., it is common to create branches when fixing bugs for a previous release of a software project, while simultaneously developing new features for the next project version.

Git distinguishes between two kinds of branches: 
- *Local branches* - these are branches in your local repository. If you have not pushed this branch to a remote repository, the branch will only be visible on your local computer.
- *Remote branches* - these are branches stored on the remote repository. These branches will be visible to everyone with access to the remote, and remote branches will become available on your local repository when you Clone a remote repository.
You can't work directly on remote branches, instead, you will need to clone the remote repository in order to work on the branch.

## Cloning, Tracking and Local Branches
When you use `git clone` to [Clone](Clone.md) a remote repository, all remote branches will become known to the local repository (known as 'remote-tracking' branches).

Remote-tracking branches will have the name of the remote prepended, e.g. `origin/main`.

When you checkout from a remote tracking branch (e.g. `git checkout origin/main -b main`) when checking out a local branch, Git will link the local branch to the remote-tracking branch (known as the 'upstream' for the local branch), so that when you `push`, Git will know to push the commits to the original remote branch (unless you specify otherwise), and if you `pull`, Git will know which remote branch to monitor for new commits.

You can also elect to create a local branch which does not track a remote branch (`git checkout -b mybranch`), which means you'll take manual ownership of merging remote changes into your local branch, or providing a target remote branch when pushing.

After Cloning, Git will checkout the default local branch into your Working Tree - this is usually *main* (or *master* in older repositories).

## Working with Branches
> **TODO** Discuss with Syntevo - it's extremely difficult to explain the checkout options without either a SmartGit screenshot (in which case this is part of the GUI, no longer a concept), or via the git bash command line, as I've done below.

The `checkout` command is used to switch between branches in Git.

For existing local branches, checkout will simply switch the Working Tree to the branch selected, e.g.

`git checkout ExistingFeature`

When creating new branches, unless you specify a starting point, Git will assume your new branch should be created from the current branch (referred to as `HEAD`):

`git checkout -b NewFeature` 

To create new local branches from existing remote branches, you'll need to specify the remote tracking branch as the starting point, e.g.

`git checkout -b NewFeature origin/main`

will create a local branch `NewFeature` which tracks the upstream `origin/main`. (Note : In some teams, development etiquette requires that you `reserve` the new branch name on the remote before checking it out locally).

In addition to checking out existing remote branches, Git also allows you to create new local branches from an existing commit hash, or tag, e.g.

`git checkout -b NewFeature ce1067054f`

Where `ce1067054f` is the SHA hash of the commit that you would like the `NewFeature` local branch to be created from.
#### Tip
>
> After a creating a new release, it is good practice to tag the commit which produced that release with an identifier for that release.
This will make it easier to identify where to branch from when creating bug fix commits for that release.
>

When you push changes from your local branch to the origin repository,
these changes will be propagated to the tracked (remote) branch as well.
Similarly, when you pull changes from the origin repository, these
changes will also be stored in the tracked (remote) branch of the local
repository. To get the tracked branch changes into your local branch,
the remote changes have to be *merged from the tracked branch*. This can
be done either directly when invoking the *Pull* command in SmartGit, or
later by explicitly invoking the *Merge* command. An alternative to the
Merge command is the Rebase command.


#### Tip
>
>The method to be used by Pull (either *Merge* or *Rebase*) can be
>configured in **Repository\|Settings** on the **Pull** tab.
>

## Branches are just pointers to commits

**TODO** Simplify this wording. The HEAD is the pointer stored in the local repository representing 'what' has been checked out in the Working Tree. 
This can be branch, or to a specific commit (in which case the state is referred to as detached HEAD).


Every branch is simply a named pointer to a commit. A special unique
pointer for every repository is the *HEAD* which points to the commit
the working tree state currently corresponds to. The HEAD cannot only
point to a commit, but also to a local branch, which itself points to a
commit. Committing changes will create a new commit on top of the commit
or local branch the HEAD is pointing to. If the HEAD points to a local
branch, the branch pointer will be moved forward to the new commit; thus
the HEAD will also indirectly point to the new commit. If the HEAD
points to a commit, the HEAD itself is moved forward to the new commit.
