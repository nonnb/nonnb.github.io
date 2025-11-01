# Git Pull

The `git pull` command is used to [fetch](GitFetch.md) and [integrate changes](Merging.md) from a remote repository into your current branch in your local repository.

Depending on your configuration, `git pull` can be thought of as a combination of two commands:

`git fetch`

Followed by either:

`git merge` or `git rebase`

The decision whether to [merge](Merging.md) changes or [rebase](Rebasing.md) new commits in your current branch on top of the fetched changes can be controlled e.g., by specifying the `--rebase` option:

`git pull --rebase`

Alternatively, you can set the `pull.rebase` configuration option in your Git configuration, which will make all further pulls default to using rebase.

#### Note
> - `git pull` can only fast-forward commits if there are no new commits on your local branch since the last common ancestor with the remote branch.
> - Using `git pull` with merge will create a new merge commit if there are new commits on both the remote branch and your local branch.
> - If you have uncommitted changes in your working directory, `git pull` may fail unless you stash or commit those changes first.
> - If there are conflicting changes between the remote branch and your local branch, you Working Directory will be left in a [Merging status](Working-Tree-States.md#merge-conflicts-merging-status). 
> You will need to use a tool like [SmartGit Conflict Resolver](../GUI/Branch/Conflict-Solver.md) to resolve the conflicts before completing the merge or rebase.
