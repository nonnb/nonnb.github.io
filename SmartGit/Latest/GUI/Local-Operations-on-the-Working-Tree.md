---
redirect_from:
  - /SmartGit/Latest/Local-Operations-on-the-Working-Tree
  - /SmartGit/Latest/Local-Operations-on-the-Working-Tree.html
---
# Local Operations on the Working Tree

## Stage, Unstage, and the Index Editor

Git's [Index](../GitConcepts/The-Index.md) tracks which changes in the Working Tree have been selected to be included in the next commit. 

SmartGit provides following facilities to modify this selection:

-   **Stage and Unstage commands** allow you to add and remove all changes made to a file to and from the Index, respectively.
-   **Changes View** allows you to add or remove only `hunks` (i.e. parts of the file) to and from the Index (`git add -i`)
-   **Index Editor** allows you to directly edit the contents of the Index for a certain file, thereby adding or removing arbitrary
    content to and from the Index.

Depending on whether a file is already tracked or not:
- If you invoke Stage on an untracked (new) file, e.g. via **Local\|Stage**, that file will be scheduled for addition to the repository.
- If Stage is invoked on an already-tracked file, changes made to the file will be scheduled for the next commit any changes made to the file, including its removal.

Conversely, the Unstage command (**Local\|Unstage**) will remove the selected file from in the Index, and any changes will not be part of the next commit.

Similarly, staging and unstaging hunks from the **Changes** view will schedule or un-schedule parts of these files which have been changed, for the next commit.

If you select a file and invoke the Index Editor, e.g. via **Local\|Index Editor**, the Index Editor window will appear.

The Index Editor is a three-way diff view on the selected file, where the three editors represent:
- the file's state in the Repository
- the Index
- the Working Tree

You can edit the file contents in the Index and the Working Tree (but not the version in the Repository, obviously), and move changes between these two editors by clicking on the arrow and \`x' buttons to move changes between the views.

Lastly, to commit staged changes, select the working tree root in the **Repositories** view and invoke the [Commit](#commit) command (see below).

## Ignore

The **Local\|Ignore** command indicates that the selected untracked files should be marked as `ignored`.

`Ignore` is useful for preventing files in the local Working Tree, such as compiled output, binary, debugging, and runtime log files, that should not be added to the repository.
Ignoring a file will prevent it from showing up as \`untracked' in future, which reduces visual clutter and reduces the chance of unwanted files being added to the repository. 
If the Files view option **Show Ignored Files** is selected, ignored files will be shown.

#### Note
>
>
>**Show Ignored Files** will only display ignored files in versioned directories.
>Ignored files or sub-directories in ignored directories won't show up,
>as SmartGit will not even scan into these directories for performance reasons.
>

When you mark a file in SmartGit as `ignored`, an entry will be added to the `.gitignore` file in the same directory.
The `.gitignore` file will be added to the repository if it isn't already present. 
With the SmartGit Ignore command you can only ignore files in the current directory.
To use more advanced Git ignore options, you may need to edit the `.gitignore` file(s) by hand, which will allow advanced patterns, such as entire folders, and files matching wild card patterns to be ignored.

#### Tip
> To understand by which configuration an *ignored* file is becoming
> ignored, use **Local\|Edit Ignore File**.

## Assume Unchanged

Invoke **Local\|Toggle 'Assume Unchanged'** (`assume-unchanged`) on a selection of modified files to ignore any local modifications to the file (e.g. if a developer should never change this file).
Files which are `assumed unchanged` won't be detected as modified afterwards and hence won't be included in the next commit.

To turn a file back into *Modified* state, use **Toggle 'Assume Unchanged'** on an *Assume-Unchanged* file again. 
If the **Files** view option **Show Assume-Unchanged Files** is selected, *Assume-Unchanged* files will be shown.

## Skipped

Invoke **Local\|Toggle 'Skip Worktree'** (`--skip-worktree`) on a selection of files to skip them from being added to the *Index*. 
This is similar to [Assume Unchanged](#assume-unchanged) , but in general more persistent in case of commands like **Reset**.

To get a file back into the Index, use **Toggle 'Skip Worktree'** on a *Skipped* file again. 
If the Files view option **Show Skipped Files** is selected, *Skipped* files will be shown.

## Commit
The Commit command (**Local\|Commit**) is used for creating a new commit from staged changes in the local repository.

If the working tree is in *merging* or *rebasing* state (see [Merge](Merge.md) and [Rebase](Rebase.md)), you can only commit the entire working tree.

Otherwise, you can select the files to commit.
Previously tracked, but now missing files will be removed from the repository, and untracked new files will be added. 
This behavior can be changed in the Preferences, section **Commands**.

If you have [staged changes in the Index](#stage-unstage-and-the-index-editor), you can commit them by selecting at least one file with Index changes or by selecting the working tree root before invoking the Commit command.

While entering the commit message, you can use *\<Ctrl>+\<Space>*-keystroke to auto-complete file names or file paths.

Use **Select from Log** to pick a commit message or SHA ID from the Log.
By default, SmartGit will 'guide' you to write commit messages in a standardized format, which will not exceed certain line lengths. 
You can disable this line length guide in **Edit\|Preferences**.

If **Amend last commit** is selected, you can amend the previous commit and combine it with the current commit, e.g. to add a forgotten file. 
By default, this option is only available for commits not yet pushed.
You can enable this option for already pushed commits in Preferences, section **Commands**.
When amending a commit, you have the option to replace, or reuse the commit message on the previous commit.

**Note:** Amend last commit is equivalent to removing the previous commit, and replacing it with a new commit representing changes made in both commits. 
This is why amending a commit which has already been pushed to a remote repository is not advised.

If you commit while the working tree is in *merging* state, you will have the option to create either a merge commit or a normal commit. 
See [Merge](Branching/Merge.md) for details.

#### Note
>
>If the commit fails because Git complains "unable to auto-detect email address",
>you should set your name and email address in the [Repository Settings](Repository/Repository.md#settings) .
>

## Altering Local Commits

SmartGit provides several ways to make alterations to local commits:

-   **Undo Last Commit** will undo the last commit. The contents of the last commit will be moved to the [Index](The-Index.md), so no changes will be lost.
-   **Edit Commit Message** allows you to edit the commit message of the last commit.
    In the **Journal** view on the working tree window or the **Graph** view of the log window, you can edit the commit message of
    any of the local commits by selecting the commit and invoking **Edit Commit Message** from the commit's context menu.
-   **Squash Commits** allows you to combine a range of local commits into a single commit, by selecting the commit range in the **Journal** view off the
    working tree window or the **Graph** view of the log window, and then invoking **Squash Commits** from the context menu of the commit range.
-   **Reorder Commits** - In the **Journal** view of the working tree window or the **Graph** view of the log window you can drag & drop a
    commit to another location in the list to effectively change its position.

#### Warning
>
>Do not undo a commit which has already been pushed to a remote repository unless you know what you're doing!
>If you do this, you will need to force-push your local changes, which might
>discard other users' commits in the remote repository.
>

## Discard

Use **Local\|Discard** to revert the contents of the selected files either back to their [Index](The-Index.md) state, or back to their repository state (HEAD). 
If the Working Tree is in a *merging* or *rebasing* state, this command can be used on the root of the Working Tree to get out of the *merging* or *rebasing* state.

## Remove

Use **Local\|Remove** to remove files from the local repository and optionally to delete them in the working tree.

If the local file in the working tree is already removed, [staging](#stage-unstage-and-the-index-editor) the file deletion will have the same
effect, however, the Remove command also allows you to remove files from the repository while keeping them locally.

## Moving/Renaming Files

In general, Git's move/rename tracking happens always on-the-fly, e.g. when logging or blaming a file.
Hence, there is no need for an explicit *move* operation: just move your files with your favorite tools (IDE,
file explorer, from command line).

However, Git does possess a `git move` command for convenience which performs a normal file system move and then stages the removed and the newly added
file to the *Index*.
For a GUI client like SmartGit, providing such an operation is not usually necessary. But due to demand from users for the missing `move` operation, SmartGit provides **Local\|Move or Rename**.

## Delete

Use **Local\|Delete** to delete local files (or directories) from the working tree.
You either may delete the files directly or move them to the trash.

## Stashes

Stashes are a convenient way to put the current working tree changes or just some selected files aside and re-apply them later.

Use **Local\|Stash All** to stash away all local modifications of your working tree.
To stash away only the selected files, use **Local\|Stash Selection**. The resulting stash will show up in the **Branches** view.


#### Note
>
>The option **Include untracked files** (Preferences, page **Commands**)
>is convenient to include *untracked* files for the stash as well.
>Depending on the operating system it may take significantly longer to execute the operation.
>

Right-click the stash and select **Apply Stash** to re-apply the contained changes to your Working Tree (e.g. after switching branches).
To get rid of obsolete stashes, use **Drop Stash**, however be aware that this will irretrievably get rid of the changes which are stored in the stash. 
The **Rename Stash** command allows you to change the displayed stash message.

## Run Garbage Collector

The Git Garbage Collector usually runs in the background, however, you can choose to explicitly execute the **Run Garbage Collector** command to force the garbage collector (`git gc`) to run immediately.

The Git Garbage Collector performs housekeeping tasks such as deleting commits which are no longer referenced in the repository, such as :
- commits which have been rebased
- commits which have been amended and rewritten to a new commit
- commits which have been squashed

You can view commits eligible for garbage collection in SmartGit's Log by selecting the **Recyclable Commits** option in the *Branches* view.
