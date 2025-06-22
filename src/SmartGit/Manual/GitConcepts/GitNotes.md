# Git Notes

An often overlooked feature in Git is `git notes`, which allows text or binary meta-data to be attached to a commit.
As git notes are linked to an existing commit, rather than part of the commit, it means notes can be added and removed after the commit is created, and does not modify the commit history of the target commit.

## Example uses for git notes

- References to requirements (as an alternative to using [BugTraq](../Integrations/Bugtraq-links-to-issue-trackers.md) to link to a ticketing in a commit message)
- Linking peer or AI code review comments to a commit
- Performing distributed code reviews without requiring additional persistence in a git hosting service such as GitHub or Bitbucket, e.g. [git-appraise](https://github.com/google/git-appraise)

## Implementation
Git notes works by creating a parallel `/refs/notes/<category>` reference in the repository, where `<category>` is the customizable 'type' of note that is to be added.

If no refs category is specified, git will default `<category>` to **commits**.

Each time a note is added or removed from `<category>`, a commit is added into `/refs/notes/<category>`.

For example:

`git notes add -m "Commit released on 2025-03-22"`

will do the following:

- Create a new refs in the repository for the default 'commits' category `refs/notes/commits`
- Create a new commit on this ref `refs/notes/commits`

#### Notes
> There are certain limitations with the git notes design which should be understood:
> - Only one note can be attached per refs Category per commit.
>   Additional notes metadata can be attached to a different commit, or different category, OR, the existing note will need to be amended to include the new metadata.
> - As notes are not part of the HEAD / branch commit history, notes are not pushed or fetched by default unless configured to to do.
>   Git refs containing notes will need to be pushed separately, e.g.
>   `git push origin refs/notes/commits`
> - As with any file under version control, conflicts can occur when two or more independent note changes or additions  have been made to the the same commit and refs category.
>   Please consult the available [notes merge strategies](https://git-scm.com/docs/git-notes#Documentation/git-notes.txt-merge) to choose an appropriate resolution strategy in your repository.

### Removing Git Notes support from a repository
Deleting all git notes in a category from a repository does not by itself remove the `refs/notes/<category>` ref from the repository.
As a result, SmartGit will still enable git notes functionality if the `refs/notes/commits` ref is still present in the repository, even if no notes are present.

To completely remove notes support, run the following `git update-ref -d` command in the repo, e.g. to remove the default `commits` category:

`git update-ref -d refs/notes/commits`
