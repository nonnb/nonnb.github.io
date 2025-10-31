# Git Fetch

The [`git fetch`](https://git-scm.com/docs/git-fetch) command is used to retrieve new commits, branches, and tags from one or more remote repositories
into your local repository, without merging them into your current branch.

This allows you to compare changes on the remote before deciding to integrate them into your local work.

When you run `git fetch`, Git contacts the remote repository and downloads any new data that has been added since your last fetch or pull. 
This includes new commits on branches, new branches, and new tags. 

The fetched data is stored in your local repository's remote-tracking branches (e.g., `origin/main` for the `main` branch on the `origin` remote).    

`git fetch -all`

- Fetches new commits from all configured remotes.

`git fetch <remote>`

- Fetches new commits from the specified remote.

`git fetch <remote> <branch>`

- Fetches new commits from the specified remote and branch only.

`git fetch --tags`

- By default, only tags that are reachable from branches in your local repository are fetched.
  However, the `--tags` option allows you to fetch all tags from the remote repository.

#### Note:

> It is possible to adapt default behavior of `git fetch` by modifying the [`fetch` setting](https://git-scm.com/docs/git-fetch#_named_remote_in_configuration_file) for a specific remote in your Git configuration, beneath the `[remote "<remote>"]` section.
