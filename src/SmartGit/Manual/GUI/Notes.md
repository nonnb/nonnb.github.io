# Working with Git Notes
Smart Git supports the [git notes](../GitConcepts/GitNotes.md) feature available in Git, which allows additional information such as metadata to be associated with a commit.

Notes can be used for many different purposes, such as:
- Storing reference information to requirements (as an alternative to using [BugTraq](../Integrations/Bugtraq-links-to-issue-trackers.md) to link to a ticketing in a commit message)
- Linking peer or AI code review comments to a commit e.g. [git-appraise](https://github.com/google/git-appraise) without requiring additional persistence in a git hosting service 
  such as GitHub or Bitbucket.
- SmartGit's AI commit annotation **TODO LINK** feature makes use of notes to store AI-generated annotation markers.

Although git's notes feature only allows one note per commit per category, if required, additional categories can be to allow multiple notes can be associated with the same commit.
**TODO LINK TO Marc's Integrations/Notes config*

SmartGit's git notes support includes the following features:
- The ability to add and remove notes through the UI
- The ability to add new categories of note [through configuration](../Integrations/Notes.md)
- The ability to synchronize notes with a remove using the **Other Refs** section of the **Branches View**

**TODO : Merge Marc's notes configuration documentation into this repo.
Current Location is here
https://github.com/syntevo/docs/blob/feature/marc/ai-and-notes/src/SmartGit/Manual/Integrations/Notes.md

#### Note
> - Git notes are not automatically pushed or fetched from the remote by default.
>   However, it is possible to configure your local repository to automatically synchronize note refs any time push and fetch activity is performed 
>    - please [consult this reference](../GitConcepts/GitNotes.md#configuring-automatic-remote-note-synchronization).
> - Not all Git hosting services will show notes on their web portal UI. 
>   However, all major hosting services will retain the notes refs where they can be synchronized with other repositories.
> - SmartGit refers to the default `commits` notes category ref as `Notes` on the UI
> - Not all git hosting providers provide visual support for notes pushed to their repos. 
>   However, any data you store in notes which are pushed to these remotes will still be available when fetched.

## Enabling Notes for a Repository

Unless notes have been enabled for a repository via one of the below methods, SmartGit's Notes features will not be enabled.

Notes can be enabled for a repository through one of the following methods:
- Add one or more `[smartgit-notes "<category-id>"]` sections in the git configuration file hierarchy (e.g. to the repository `.git/config` file)
** TODO REF

```ini
[smartgit-notes "Reviews"]
   ref              = review
   color            = 0000FF
```

- Or, if SmartGit detects an entry under the `refs/notes/commits` path of the repository refs, it will automatically enable notes features for the repository.
  e.g. if `git notes add ...` has previously been applied to the repository.

## Using Notes in SmartGit
Notes will appear via the **TODO-Icon icon in the color configured for the notes category, in the **Graph View** of the **Log Window** and the **Standard Window**.

- Add a new Note by selecting the target commit in the Graph View, and clicking the **Add Note...** command.
  You can then type in your note, and choose the category of note from one of the configured categories.
- Hover the mouse over the note icon to see the contents of the note.
- A Note can be removed by clicking on the note and selecting `Remove <category> note`

**TODO - Screenshot of multiple color icons, Add Note, and the Dialog in one screen?

## Troubleshooting

- The **Add Note** command does not appear when I click on a commit in the **Graph View**?

> This is because the notes feature has not been [enabled in SmartGit](#enabling-notes-for-a-repository).

- When I attempt to add a note to a commit, I receive the warning _Do you want to overwrite the existing note?_

> By design, git notes only allows a single note per commit, per category to be added.
  You can either append to the existing note and overwrite it, or you can add a new note in a different notes category.
  
- I've pushed a branch containing notes in my repository to a remote, however when others clone the repository, they do not see the notes?

> Git notes are not stored on the current branch, and must be pushed and fetched separately.
  In the **Log Window**, under the **Branches View**, open the *Other Refs* section and push the `notes/<category>` ref to the remote.
  Similarly, other users need to fetch *Other Refs* in order to obtain all notes for the repository

- I've rebased several commits containing notes using the squash option, and now I don't see my notes!

> As notes are linked to a specific commit id, rewriting commands such as rebase will create new commits.
  You can use the [notes rewriteRef configuration](GitNotes.md#rebasing-and-git-notes) to instruct git to copy (or append) notes on squashed commits across to the newly rewritten commit.
  
