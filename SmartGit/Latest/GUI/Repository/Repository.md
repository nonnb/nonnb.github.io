---
redirect_from:
  - /SmartGit/Latest/Repository-Related
  - /SmartGit/Latest/Repository-Related.html
---
# Working with Repositories

SmartGit remembers repositories that you've previously opened and any GUI-related settings applied to each repository.
To open a repository, double-click it. 
If the repository is already is open in another window, SmartGit will focus on that window.
If the current window executes commands or **Open in New Window** has been selected from the repository's context menu, the repository will open in a new window.
To open multiple repositories simultaneously, select and highlight each repository (e.g., using **`Ctrl/Cmd` + click**) and choose **Open** from the context menu.

Repositories can be arranged in groups.
Right-click on the repositories and select the target group or **New Group** from the **Move To** submenu.
Alternatively, you can use drag-and-drop onto the target group or a repository inside the target group 
(see [autoscroll](../Tips-and-Tricks.md#autoscrolling-while-drag-and-drop)).

Repositories can be marked as favorites using the **Mark as Favorite** (**Unmark as Favorite**) option. 
Favorite repositories are indicated with an asterisk (*) after the name and are sorted before non-favorite repositories. 
Additionally, favorite repositories will receive background refresh operations.

## Opening a Repository

Use **Repository \| Add or Create** to either open an existing local repository (e.g., initialized or cloned with the Git command line client) or to initialize a new repository.

Specify the local directory you want to open.
If the specified directory is not yet a Git repository, you can initialize it.

## Settings

Once you have a opened a repository, use **Repository \| Settings** to configure repository-specific settings.

**Note:** 
- To change the same repository settings as defaults across **all** repositories, please use [**Edit \| Preferences \| Commands \| Git Config**](../Preferences/Commands.md#git-config).
- You can also edit the Git condirguration by manualy updating your `.gitconfig` file.

### User Tab
You can configure your name and email address on this tab which will be used when [committing](../Local-Operations-on-the-Working-Tree.md#commit)
to this repository. 

### Fetch and Pull Tab
This tab allows you to configure options related to the [Pull command](../Synchronizing-with-Remote-Repositories.md#pull):

- Specify whether to **Merge** or **Rebase** remote changes when pulling from a remote repository.
- Choose whether to prune obsolete remote-tracked branches.
- Set Synchronization options for repositories containing submodules.

### Push Tab
This tab provides options for handling changes in submodules (applicable only to repositories containing submodules):

- **Ignore submodules** will only push changes in the current repository.
- **Abort if changes to submodules** mean you should explicitly push changes to submodules before pushing changes in the current (dependent) repository.
- **Push Submodules First** will attempt to push changes to submodules before the current repository is pushed.

### Signing Tab

This tab allows you to set up a GPG application and private key, which can be used to sign commits.

### Encoding Tab

This tab allows SmartGit to select the text file encoding used when displaying text files in the **Changes** view or **Compare** window.
Unless you have a specific reason for changing it, it is recommended that the default UTF-8 encoding be used.
SmartGit will automatically detect UTF-8 encoding, with or without leading byte order markers (BOM).

### Tag Grouping

This tab provides advanced configuration options how SmartGit groups tags, branches, or other `refs` that match this configuration.
