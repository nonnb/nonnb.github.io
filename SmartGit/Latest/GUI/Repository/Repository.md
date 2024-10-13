---
redirect_from:
  - /SmartGit/Latest/Repository-Related
  - /SmartGit/Latest/Repository-Related.html
---
# Working with Repositories

SmartGit remembers repositories that you've previously opened, and any GUI-related settings that you may have applied to each repository.
To open a repository, double-click it. 
If the repository is already is open in another window, SmartGit will focus on the existing window with the opened repository.
The repository will open in a new window if the current window is currently executing commands or if **Open in New Window** from the repository's context menu has been selected.
To open multiple repositories at once, select / highlight each repository (e.g. using `Ctrl/Cmd` + click) and choose **Open** from the context menu.

Repositories can be arranged in groups.
Right-click the repositories and select the target group or **New Group** from the **Move To** submenu.
Alternatively, you can use drag-and-drop - either onto the target group or a repository inside the target group 
(see [autoscroll](Tips-and-Tricks.md#autoscrolling-while-drag-and-drop)).

Repositories can be marked as favorite using the **Mark as Favorite** (**Unmark as Favorite**). 
Favorite repositories are indicated with an asterisk after the name, and are sorted before non-favorite repositories. 
In addition, favorite repositories will also receive background refresh operations.

## Opening a Repository

Use **Repository\|Add or Create** to either open an existing local repository (e.g. initialized or cloned with the Git command line client) or to initialize a new repository.

You need to specify which local directory you want to open.
If the specified directory is not yet a Git repository, you have the option to initialize it.

## Settings

Once you have a opened a repository, use **Repository\|Settings** to configure repository-specific settings for this repository.

**Note:** To change the same repository settings as a default across ALL repositories, please use [**Edit\|Preferences\|Commands\|Git Config**](../Preferences/Commands.md#git-config).

### User Tab
On this tab you can configure your name and email address that will be used when [committing](Local-Operations-on-the-Working-Tree.md#commit)
for this repository. 

To change the global settings, select **Remember as default** - this will then be applied for your work in all repositories, by updating your `.gitconfig` file.

### Fetch and Pull Tab
This tab allows configuring of options related to the [Pull command](../Synchronizing-with-Remote-Repositories.md#pull):

- Specify whether to Merge or Rebase remote changes when Pulling a remote repository
- Whether to prune obsolete remote tracked branches
- Synchronization options for repositories containing submodules

### Push Tab
This tab provides options when changes are made to submodules (applicable only to repositories containing submodules):

- **Ignore submodules** will only push changes in the current repository.
- **Abort if changes to submodules** means you should explicitly push changes to submodules before pushes in the current (dependent) repository.
- **Push Submodules First** will attempt to push changes to submodules before the current repository is pushed.

### Signing Tab

This tab allows you to set up a GPG application and private key which can be used to sign commits that you make.

### Encoding Tab

This tab allows selection of the Text File encoding used by SmartGit when showing text files in the **Changes** view or **Compare** window.
Unless you have a specific reason to do otherwise, it is recommended that the default UTF-8 encoding be used.
SmartGit will automatically detect UTF-8 encoding with or without leading byte order markers (BOM).

### Tag Grouping

This tab allows advanced configuration of how SmartGit will group Tags, Branches or other `refs` matched in this configuration.
