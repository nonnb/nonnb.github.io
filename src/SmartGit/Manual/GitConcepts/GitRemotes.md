# Git Remote Repositories (Remotes)

Although much of Git's functionality is designed to work within a local repository, you will need to synchronize your commits with 
remote repositories in order to collaborate with other developers.

## Common Commands for Working with Remotes:

### Clone

`git clone <url>` 

Creates a local copy of a remote beneath the current folder.

By default, the local repository will be created in a sub folder with the same name as the repository.
Use `git clone <url> <folder>` to override the folder name.

### Add a new remote

`git remote add <remote> <url> `

Will create a link between your local repository and a remote.
This command is useful if you have recently created a new local repository (e.g. with `git init`), or, if you wish to synchronize with more than one remote (e.g. see Forking, below)

By convention, the default remote name alias is `origin`, however, you can provide a different name for a remote, 
which can be important if your repository is connected to more than one remote.




- [`git fetch`](GitFetch.md) with [`git merge`](Merging.md) or [`git rebase`](Rebasing.md), 

  OR [`git pull`](GitPull.md) can be used used to retrieve changes from a remote and then integrate these into a branch in your local repository.

- [`git push`](GitPush.md) is used to synchronize new commits in your local repository to a remote.


`git remote -vv`

- Lists all remotes linked to your local repository, along with their URLs


### Forking

Often, when working in private repositories, authorized developers will have sufficient access to create new feature branches and to push new commits to existing branches directly to the remote.
Some Git hosting providers (like GitHub) will allow the repository owner to protect important branches (e.g. `master` or `main`) from direct pushes.
In this case, after pushing changes to a feature branch, a pull request can be created between the two branches, where changes can be reviewed, and merged or fast forwarded once accepted.

However, on many public and open source repositories, only authorized contributors will be permitted to create branches or create commits to the repository.
In this case, the repository can still be cloned by the developer, however the developer will be required to Fork the repository.
Any new commits made by the developer will need to be pushed to the forked repository, and a Pull Request can then be created between branches in the forked repos.
The original repository contributors 

With forking









