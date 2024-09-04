# Git for Subversion Users

If you are familiar with traditional, Centralized Version Control System such as Subversion (SVN), there are some conceptual differences that you'll need to understand in order to adapt to the basic flow in Git.

## Remote and Local Repositories and the Working Tree

Subversion (SVN) requires the use of "working copies" of a remote (server) repository, each of which corresponds to exactly one repository (SVN working copies will contain the entire repository, or just parts of it).

In Git, the equivalent of a `working copy` is the [Working Tree](Working-Tree-States.md), one of the most important features your local repository (remember, in a Distributed Version Control System like Git, there isn't a single, central repository - by Cloning a remote repository, you get a copy of the repository).

Just like the working copy in SVN, the Git Working Tree is the directory where you can edit files, build and test software, before commiting changes. 

## Cloning, Checkout, Commiting and Pushing in Git

Although the outcomes are similar in both Git and SVN (i.e. adding new commits to a branch on a remote server), in Git, there are some conceptual differences that you'll need to be aware of:
- In Git, you [Clone](Clone.md) a repository from a remote server. This is somewhat similar to checking out an SVN branch onto your local system for the first time.
- In Git, you use Checkout to switch between branches in your local repository. This is somewhat similar to using the `switch` command in SVN, although note that Git changes branch on your local repository.
- In SVN, using 'commit' will publish your local changes to the remote server. In Git, this activity is broken down into smaller, distinct steps:
  - [Staging](The-Index.md) - this is a Git process where you decide WHICH of the changes you've made in your Working Tree that you'd like to be added to the next commit. Unless you stage the files that you've changed, added or deleted, these will be left out of the next commit.
  - [Commit](Commits.md) - in Git, commit will add the file changes that you've staged and create a new commit on the current branch, on your local repository.
  - Push - Push is the command for Git to upload new commits on your local repository to a remote repository (e.g. back to the `origin` repository). Git keeps track of the remote branch from which your local branch originated, and by default will push changes back to this branch. However, with Push, you also have the option of overriding the branch in the remote repository to which you'd like to push your commits. 
 - In Git, doing a Pull is similar to the SVN `refresh` command, allowing new commits (since your last Clone or Pull) in the tracked remote branch to be merged into your working directory. Git Pull is equivalent to `Fetch` (bring your local repository up to date with the remote) and `Merge` (merge changes on the tracked branch into your local branch)
