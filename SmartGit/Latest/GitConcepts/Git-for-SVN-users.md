## Repository, Working Tree, Commit

Traditional centralized version control systems such as Subversion (SVN) require the use of "working copies" of a remote (server) repository, each of which corresponds to exactly one repository (SVN working copies will contain the entire repository, or just to parts of it).

In Git, the equivalent of a `working copy` is the Working Tree, which is part of your local repository (remember, in a Distributed Version Control System like Git, there isn't a single, central repository).

Just like the working copy in SVN, the Git Working Tree is the directory where you can edit files, build and test software, before commiting changes. 

However, in Git, there are some changes that you'll need to be aware of:
- In Git, you [Clone](Clone.md) a repository from a remote server. This is somewhat similar to checking out an SVN branch onto your local system for the first time.
- In Git, you use Checkout to switch between branches in your local repository. This is somewhat similar to using the `switch` command in SVN, although note that Git changes branch in your local repository.
- In SVN, using 'commit' will publish your local changes to the remote server. In Git, this activity is broken down into smaller, distinct steps:
  - Staging - this is a Git process where you decide WHICH of the changes you've made in your Working Tree that you'd like to be added to the next commit. Unless you stage the files that you've changed, added or deleted, these will be left out of the next commit.
  - Commit - in Git, commit will add the file changes that you've staged and create a new commit on the current branch, on your local repository.
  - Push - Push is the command for Git to upload new commits on your local repository to a remote repository (e.g. back to the `origin` repository). Git does keep track of the remote branch from which your local branch originated, and will default to pushing changes back to this branch. When Pushing in Git, you also have the option of overriding the branch in the remote repository to which you'd like to push your commits. 
