# Git Notes

An often overlooked feature in Git is `git notes`, which allows text or binary meta-data to be attached to a commit.
As notes are linked to an existing commit, and do not affect the commit history of the working branch, 
notes can be added and removed after the commit is created without modify the branch's commit history.

## Example uses for git notes
Sample usages of git notes:
- For storing reference information to requirements (as an alternative to using [BugTraq](../Integrations/Bugtraq-links-to-issue-trackers.md) to link to a ticketing in a commit message)
- Linking peer or AI code review comments to a commit e.g. [git-appraise](https://github.com/google/git-appraise) without requiring additional persistence in a git hosting service 
  such as GitHub or Bitbucket.

## Implementation
Git notes works by creating a parallel `/refs/notes/<category>` reference in the repository, where `<category>` is the customizable 'type' of note that is to be added.

If no refs category is specified, git will default `<category>` to **commits** (the category default can be overridden with the `GIT_NOTES_REF` environment variable or by setting the `core.notesRef` config value).

Each time a note is added or removed from `<category>`, a commit is added into `/refs/notes/<category>`.

For example:

`git notes add -m "Build released on 2025-03-22"`

will do the following:

- Create a new refs in the repository for the default 'commits' category `refs/notes/commits` (if it does not already exist)
- Create a new commit on this ref `refs/notes/commits`.
  Commits on the notes refs are orphaned from your usual code base branch refs.

Using the `--ref <category>` option allows you to add a note to the specified category ref, e.g.

`git notes --ref reviews add -m "Please remove unused imports on MyFile.java"`

#### Note
> - Like tags, by default, notes are not pushed or fetched by default when you synchronize your branches to a remote.
>   Notes will require manual synchronization with the remote, OR configuration changes need to be made to automatically synchronize notes with the remote.
>   e.g. Manually push notes in the default _commits_ category to the _origin_ remote:
>  `git push origin refs/notes/commits`
>
>  In general, it may be simpler to [configure the repo to automatically push and fetch all notes](#configuring-automatic-remote-note-synchronization)
>
>  Similarly all note category refs can be fetched from the remote:
>  `git fetch origin 'refs/notes/*:refs/notes/*'`
>
> - There are certain limitations with the git notes design which should be understood:
>   - Only one note can be attached per refs Category per commit.
>     Additional notes metadata can be attached to a different commit, or different category, OR, the existing note will need to be amended to include the new metadata.
>   - As with any file under version control, conflicts can occur when two or more independent note changes or additions  have been made to the the same commit and refs category.
>     Please consult the available [notes merge strategies](https://git-scm.com/docs/git-notes#Documentation/git-notes.txt-merge) to choose an appropriate resolution strategy in your repository.
>   - As commits are rewritten during rebasing operations such as squash, notes associated with rewritten commits will become orphaned and will not be associated with the rebased commit.

### Configuring automatic remote note synchronization

By amending the configuration for a remote's `fetch` and `push` settings, it is possible to ensure notes remain synchronized with the remote whenever a push or fetch is performed.

```ini
[remote "origin"]
  url = ...
  ...
  fetch = refs/notes/*:refs/notes/*
  push = refs/notes/*:refs/notes/*
```

Using the _<category>_ name, or the `*` wildcard to specify which categories of note are to be synchronized.

### Rebasing and Git Notes
As notes are attached to specific commit ids, any time the commit history is rewritten, e.g. to squash or other rebase activity, 
any notes attached to rewritten commits will become orphaned from the resulting commit.

This orphan note behavior can be changed by adding a _rewriteRef_ configuration for the repository, e.g.:

```ini
[notes]
  rewriteRef = refs/notes/*
```

Will cause any notes on rewritten commits to be copied to the rewritten commit after a rebase.
If there is more than one note in the same category to be copied to the rewritten commit, the contents of the notes will be appended in sequence and attached to the new commit.

### Removing Git Notes support from a repository
Deleting all git notes in a category from a repository does not by itself remove the `refs/notes/<category>` ref from the repository.
As a result, SmartGit will still enable git notes functionality if the `refs/notes/commits` ref is still present in the repository, even if no notes are present.

To completely remove notes support, run the following `git update-ref -d` command in the repo, e.g. to remove the default `commits` category:

`git update-ref -d refs/notes/commits`
