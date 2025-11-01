# Git Fetch

The [`git fetch`](https://git-scm.com/docs/git-fetch) command is used to retrieve new commits, branches, and tags from one or more remote repositories
into your local repository, without merging them into your current branch.

This allows you to review changes on the remote before deciding whether to integrate them into your local work.

When you run `git fetch`, Git contacts the remote repository and downloads any new data added since your last fetch or pull. 
This can include
- New commits on existing branches
- Newly created branches
- New tags 

The fetched data is stored in your local repository's remote-tracking branches (e.g., `origin/main` for the `main` branch on the `origin` remote).    

**##Common Usage##**

`git fetch -all`

- Fetches new commits from all configured remotes.

`git fetch <remote>`

- Fetches new commits from the specified remote.

`git fetch <remote> <branch>`

- Fetches new commits only from the specified remote and branch.

`git fetch --tags`

- By default, only tags reachable from branches in your local repository are fetched.
The `--tags` option allows you to fetch all tags from the remote repository.

#### Note:

> You can modify the default behavior of `git fetch` by changing the [`fetch` setting](https://git-scm.com/docs/git-fetch#_named_remote_in_configuration_file) for a specific remote in your Git configuration, under the `[remote "<remote>"]` section.
