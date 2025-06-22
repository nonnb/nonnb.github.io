# Working with Git Notes
Smart Git supports the [git notes](../GitConcepts/GitNotes.md) feature available in Git, which allows metadata to be associated with a commit.
Multiple notes can be associated with a commit by creating separate categories for each type of note.

SmartGit's Git supports the following notes features:
- The ability to add and remove notes through the UI
- The ability to add new categories of note [through configuration](../Integrations/Notes.md)

#### Note
- Notes are not automatically pushed to the remote
- Not all Git hosting services will show notes on their web portal UI

## Enabling Notes for a Repository

Notes can be enabled for a repository through one of the following methods:
- Adding a `[smartgit-notes "<category-id>"]` section in the git configuration file hierarchy (e.g. the repository `.git/config`
- SmartGit will automatically enable notes features for a repository when it detects an entry under the `refs/notes/commits` path of the repository refs, e.g. if a `git notes add ...` command.

