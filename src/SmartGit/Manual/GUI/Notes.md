# Working with Git Notes
Smart Git supports the [git notes](../GitConcepts/GitNotes.md) feature available in Git, which allows metadata to be associated with a commit.

If required, Multiple notes can be associated with a commit by creating separate categories for each type of note.
SmartGit's Git supports the following notes features:
- The ability to add and remove notes through the UI
- The ability to add new categories of note [through configuration](../Integrations/Notes.md)
- The ability to synchronize notes with a remove using the **Other Refs** section of the **Branches View**

**TODO : Merge Marc's notes configuration documentation into this repo.
Current Location is here
https://github.com/syntevo/docs/blob/feature/marc/ai-and-notes/src/SmartGit/Manual/Integrations/Notes.md

**TODO Potentially, this isn't really an 'integration' as this is core capability of git - possibly move these configurations under the **Advanced Settings** section?

#### Note
- Notes are not automatically pushed or fetched from the remote by default.
  However, it is possible to configure your local repository to automatically synchronize note refs any time push and fetch activity is performed - please [consult this reference](../GitConcepts/GitNotes/).
- Not all Git hosting services will show notes on their web portal UI. However, all major hosting services will retain the notes refs where they can be synchronized with other repositories.
- **TODO - Confirm with Marc that the default 'commits' note category has been renamed to `Notes` on the UI (makes sense)

**TODO - As far as I know, GitHub removed UI support for Notes on their portal several years ago, and Azure DevOps doesn't seem to show notes when `/refs/notes/*` has been pushed to the remote.
Both hosts do however retain the refs albeit invisibly.

## Enabling Notes for a Repository

Unless notes have been enabled for a repository, SmartGit's Notes features will not be enabled.

Enable notes for a repository through one of the following methods:
- Add one or more `[smartgit-notes "<category-id>"]` sections in the git configuration file hierarchy (Repository `.git/config` is recommended)
- SmartGit will automatically enable notes features for the repository when it detects an entry under the `refs/notes/commits` path of the repository refs, 
  e.g. if a `git notes add ...` command has been applied to the repository.

## Using Notes in SmartGit
Notes will appear via the **TODO-Icon icon in the color configured for the notes category, in the **Graph View** of the **Log Window** and the **Standard Window**.

- Add a new Note by selecting the target commit in the Graph View, and clicking the **Add Note...** command.
  You can then type in your note, and choose the category of note from one of the configured categories.
- Hover the mouse over the note icon to see the contents of the note.
- A Note can be removed by clicking on the note and selecting `Remove <category> note`


**TODO - Confirm with Marc no intention to add Notes to the Journal view in the Working Tree window.
**TODO - Screenshot of multiple color icons, Add Note, and the Dialog in one screen?

## Troubleshooting

- The **Add Note** command does not appear when I click on a commit in the **Graph View**?

  This is because the notes feature has not been [enabled in SmartGit](#enabling-notes-for-a-repository).

- When I attempt to add a note to a commit, I receive the warning _Do you want to overwrite the existing note?_

  By design, git notes only allows a single note per commit, per category to be added.
  You can either append to the existing note and overwrite it, or you can add a new note in a different notes category.
  
- I've pushed a branch containing notes in my repository to a remote, however when others clone the repository, they do not see the notes?

  Git notes are not stored on the current branch, and must be pushed and fetched separately.
  In the **Log Window**, under the **Branches View**, open the *Other Refs* section and push the `notes/<category>` ref to the remote.
  Similarly, other users need to fetch *Other Refs* in order to obtain all notes for the repository

- I've rebased several commits containing notes using the squash option, and now I don't see my notes

  **TODO - I guess SmartGit could assist by merging all notes on the squashed commits and appending it to the rewritten commit as a note in the same category?
