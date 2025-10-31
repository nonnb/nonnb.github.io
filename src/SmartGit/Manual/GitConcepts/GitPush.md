# Git Push

The `git push` command is used to upload new commits which have been added to a local repository, up to a branch on a remote repository (or to multiple remotes).

Common Usages:

`git push <remote> <branch>`

- Uploads new commits in the current local branch to the specified branch on the specified remote.
  If the specified branch does not exist on the remote, a new branch with that name will be created on the remote.

`git push`

- Uploads new commits from the current local branch to its tracked branch on the default remote.
  
  The behavior of git push (with no other options) will depend on the [`push.default`](https://git-scm.com/docs/git-config#Documentation/git-config.txt-pushdefault) configuration option in your Git configuration:

  - `simple` (default): Pushes the current branch to its tracked (upstream) branch only if they have the same name.
  - `current`: If the current branch does not exist on the remote, a branch with the same name will be created on the remote.
  - `upstream`: Pushes the current branch to its tracked (upstream) branch, even if they have different names.

`git push --all <remote>`

- Pushes all local branches to the specified remote.


#### Note
> - You can only push commits to a remote repository if you have permission to do so.
> - In many hosting services, the repository owner may restrict who can push to certain branches 
    (e.g., the default branch such as `main` or `master` is often protected to prevent direct pushes). 
>   In this case, you should push your changes to a separate branch and create a pull request to allows to review your changes,
    before merging them into the main branch.
> - If the target remote branch has new commits that are not present in your local branch, the push will be rejected.
>  In this case, you will need to first [fetch](GitFetch.md) and [merge](Merging.md) / [rebase](Rebasing.md) or [pull](GitPull.md) 
   to ensure these new commits are in your local branch.