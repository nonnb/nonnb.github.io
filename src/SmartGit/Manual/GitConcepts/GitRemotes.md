# Git Remote Repositories (Remotes)

Although much of Git's functionality is designed to work within a local repository, you will need to synchronize your commits with 
Remote Repositories (remotes) in order to collaborate with other developers.
This will allow others to receive work done in the commits that you've added, and similarly, your local repository can be updated with new commits added by others.

## Common Commands for Working with Remotes:

### Cloning a remote repository

`git clone <url>` 

Creates a local copy of a remote beneath the current folder.

By default, the local repository will be created in a sub folder with the same name as the repository.
Use `git clone <url> <folder>` to override the folder name.

### Add a new remote

`git remote add <remote> <url> `

This will create a link between your local repository and a remote in your git configuration.
This command is useful if you have recently created a new local repository (e.g. with `git init`), or, if you wish to synchronize with more than one remote (e.g. see Forking, below)

By convention, the default remote name alias is `origin`, however, you can provide a different name for a remote, 
which can be important if your repository is connected to more than one remote.

### Receiving recent changes from a remote with fetch or pull

Either of the below can be used to retrieve changes from a remote and then integrate these into a branch in your local repository.

- [`git fetch`](GitFetch.md) with [`git merge`](Merging.md) or [`git rebase`](Rebasing.md), 

  OR [`git pull`](GitPull.md)

- [`git push`](GitPush.md) is used to synchronize new commits in your local repository to a remote.

### Forking

Often, when working in private repositories, authorized developers will have sufficient access to create new feature branches and to push new commits to existing branches directly to the remote.
Some Git hosting providers (like GitHub) will allow the repository owner to protect important branches (e.g. `master` or `main`) from direct pushes.
In this case, after pushing changes to a feature branch, a pull request can be created between the two branches, where changes can be reviewed, and merged or fast forwarded once accepted.

However, on many public and open source repositories, only authorized contributors will be permitted to create branches or create commits to the repository.
In this case, the repository can still be cloned by the developer, however the developer will be required to Fork the repository.
Any new commits made by the developer will need to be pushed to the forked repository, and a Pull Request (PR) can then be created between branches in the forked repos.
The original repository contributors can then review your PR and integrate your changes if accepted.

### Other useful commands when working with remotes

`git remote -vv`

- Lists all remotes linked to your local repository, along with their URLs

`git branch -r`

- Lists all branches on the remote. Adding the `-a` switch shows both remote and local branches.

`git remote set-url <remote> <url>`

- Changes the URL for a remote. This may be useful, e.g. if you change the location of your remote repositories, e.g.if moving from GitHub to BitBucket.
