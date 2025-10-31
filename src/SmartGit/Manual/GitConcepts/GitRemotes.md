# Git Remote Repositories (Remotes)

Although much of Git's functionality is designed to work within a local repository, you will need to synchronize your commits with 
remote repositories in order to collaborate with other developers.

## Common Commands for Working with Remotes:

### Clone

`git clone <url>` will create a local copy of a remote.

By default, the repository will be created in a local folder with the same name as the repository.
Use `git clone <url> <folder>` to override the folder name.

### Add a new remote

`git remote add <remote> <url> `

By convention, the default remote name alias is `origin`, however, you can provide a different name if required

- - will create a link between your local repository and a remote.
- [`git fetch`](GitFetch.md) with [`git merge`](Merging.md) or [`git rebase`](Rebasing.md), 

  OR [`git pull`](GitPull.md) can be used used to retrieve changes from a remote and then integrate these into a branch in your local repository.

- [`git push`](GitPush.md) is used to synchronize new commits in your local repository to a remote.


`git remote -vv`

- Lists all remotes linked to your local repository, along with their URLs




