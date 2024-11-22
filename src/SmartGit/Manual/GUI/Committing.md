# Committing Changes

The **Commit** command creates a new [commit](../GitConcepts/Commits.md) from [staged changes](Stage-Unstage-IndexEditor.md) in the local repository.

- It is recommended that the [**Commit View**](Commit-View.md) be used to create commits in most instances, as this allows new commits to be easily created.
- Alternatively, the **Local \| Commit** command will bring up a dialog allowing additional functionality such as re-selecting a commit message from a recent previous commit.

## Commit Basics

The following changes will be included in the commit:
- If all modified files in the *Working Tree* have been [staged in the Index](Stage-Unstage-IndexEditor.md), **Commit** will create a commit consisting of these staged changes.
- If there is a mix of staged and unstaged changes to files in the *Working Tree*, **Commit** will only commit the staged changes, and the residual changes will remain as modified files in the *Working Tree*.
- If the *Working Tree* contains modified files, however there are no staged changes, **Commit** will ask prompt whether to to automatically stage all visible modified files and then create the new commit. This has the same result as manually selecting all modified files, staging them, and then committing.

After the commit:
- New files added to the index (i.e. staged) will be added to the repository.
- Modified files will be updated in the repository.
- Previously tracked files which are deleted in the *Working Tree* and staged will be removed from the repository.

## Commit Messages

While entering the commit message, you can use *\<Ctrl>+\<Space>*-keystroke to auto-complete file names or file paths.
SmartGit will show a shortlist of files which are eligible for the commit - selecting a file will paste the name into the commit message.

Use **Select from Log** to choose a commit message or SHA ID from the Log. 

#### Tip
> - As commit messages are often shown alongside a commit hash, it is important to keep commit messages short, and to the point, so other users of the repository can quickly scan to see what changes the commit contains.
> - By default, SmartGit 'guides' you in writing commit messages in a standardized format with limited line lengths.
> You can disable this line length guide in **Edit \| Preferences**.

## Amending Commits

If **Amend last commit** is selected, you can combine the current changes with the previous commit, e.g. to add a file which was modified but not included in the previous commit.
By default, this option is only available for commits not yet pushed. You can enable this option for already pushed commits in Preferences, section **Commands**. When amending a commit, you have the option to replace, or reuse the commit message on the previous commit.

**Note:** 
> Amend last commit is equivalent to removing the previous commit, and replacing it with a new commit representing changes made in both commits.
> This is why amending a commit which has already been pushed to a remote repository is not advised.

If you commit while the working tree is in *merging* state, you will have the option to create either a merge commit or a normal commit. See [Merge](Branch/Merge.md) for details.

#### Note
> - If the Working Tree is in a *merging* or *rebasing* state (see [Merge](Branch/Merge.md) and [Rebase](Branch/Rebase.md)), you can only commit the entire working tree.
> - If the commit fails because Git complains "unable to auto-detect email address", you should set your name and email address in the [Repository Settings](Repository/Repository-Settings.md) .

## Altering Local Commits

SmartGit provides several ways to make alterations to local commits:

- **Undo Last Commit** will undo the last commit. The contents of the last commit will be moved to the [Index](../GitConcepts/The-Index.md), so no changes will be lost.
- **Edit Commit Message** allows you to edit the commit message of the last commit. In the **Journal** view on the working tree window or the **Graph** view of the log window, you can edit the commit message of any of the local commits by selecting the commit and invoking **Edit Commit Message** from the commit's context menu.
- **Squash Commits** allows you to combine a range of local commits into a single commit, by selecting the commit range in the **Journal** view off the working tree window or the **Graph** view of the log window, and then invoking **Squash Commits** from the context menu of the commit range.
- **Reorder Commits** - In the **Journal** view of the working tree window or the **Graph** view of the log window you can drag & drop a commit to another location in the list to effectively change its position.

#### Warning

>
>Do not undo a commit that has already been pushed to a remote repository unless you understand the implications.
> This could require a force-push, potentially discarding other users' commits in the remote repository.
>
