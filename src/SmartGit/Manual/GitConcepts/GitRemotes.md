# Git Remotes

Although much of Git's functionality is designed to work within a local repository, you will need to synchronize your commits with 
remote repositories ('remotes') in order to collaborate with other developers. 

Common Commands for Working with Remotes:

- Git Clone - used to create a local copy of a remote repository
- `git remote add` will create a link between your local repository and a remote repository.
- [`git fetch`](GitFetch.md) with [`git merge`](Merging.md) or [`git rebase`](Rebasing.md)
  OR [`git pull`](GitPull.md) can be used used to retrieve changes from a remote repository and then integrate these into a branch in your local repository.
Git Push is used to send your local commits to a remote repository.

  - [git clone](GitClone.md)
  - [git fetch](GitFetch.md)
  - [git pull](GitPull.md)
  - [git push](GitPush.md)

Remote repositories are versions of your project that are hosted on the internet or network somewhere. They allow multiple developers to collaborate on the same project by sharing changes.

`git remote -vv`

- Lists all remotes linked to your local repository, along with their URLs




