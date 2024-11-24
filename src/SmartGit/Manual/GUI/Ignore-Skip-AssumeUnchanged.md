# Excluding files in the Working Tree from inclusion in Staging

## Ignore

The **Local \| Ignore** command marks selected untracked files as `ignored`, which is useful for preventing files like compiled output, binary, debugging, and runtime log files from being added to the repository. Ignored files will no longer be indicated as 'untracked', so this reduces visual clutter and the risk of unintentionally adding these files.
If the option **Show Ignored Files** is selected, ignored files will still be displayed.

#### Note:

> SmartGit only displays ignored files in versioned directories.
> Ignored files or sub-directories within ignored directories are not shown for performance reasons.

When a file is marked as ignored in SmartGit, an entry is added to the `.gitignore` file in the same directory. 
The `.gitignore` file will be added to the repository if it isn't present.
To use more advanced Git ignore options, you may need to edit the `.gitignore` file(s) by hand, which will allow advanced patterns, 
such as entire folders, and files matching wild card patterns to be ignored.

#### Tip

> To view a list of ignored files or to understand why a specific file is *ignored*, use **Local\|Edit Ignore File**.

## Assume Unchanged

Invoke **Local \| Toggle 'Assume Unchanged'** (`assume-unchanged`) on selected modified files to prevent their local changes from being deleted. These files will no longer appear modified or included in the next commit.

To reverse this, toggle the command again. Those files will be displayed if the **Files View** option **Show Assume-Unchanged Files** is selected.

## Skipped

The **Local \| Toggle 'Skip Worktree'** (`--skip-worktree`) command skips selected files from being added to the *Index*. This is similar to [Assume Unchanged](#assume-unchanged) but more persistent especially for commands like **Reset**.

Use the toggle command again to bring a file back into the *Index*. Skipped files can be displayed by enabling **Show Skipped Files** in the **Files View**.
