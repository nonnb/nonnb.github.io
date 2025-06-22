# Working with Git Notes
Smart Git supports the [git notes](../GitConcepts/GitNotes.md) feature available in Git.

Benefits of using SmartGit's Git notes features
- Provides UI to allow notes to be added and viewed 
- Allows

#### Note
- Notes are not automatically pushed to the remote
- Not all Git hosting services will show notes on their web portal UI

## Enabling Notes for a Repository

Notes can be enabled for a repository through one of the following methods:
- Adding a `[smartgit-notes "<category-id>"]` section in the git configuration file hierarchy (e.g. the repository `.git/config`
- SmartGit will automatically enable notes features for a repository when it detects an entry under the `refs/notes/commits` path of the repository refs, e.g. if a `git notes add ...` command.

