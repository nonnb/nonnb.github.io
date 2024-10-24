---
redirect_from:
  - /SmartGit/Latest/Repositories-Directories-and-Files
  - /SmartGit/Latest/Repositories-Directories-and-Files.html
---
# Repository Settings

After selecting a Repository, you can use the **Repository \| Settings** menu command or the Settings context menu on the highlighted repository.
This opens a dialog to configure certain options of your repository (`<repository>/.git/config`) file.

**Note:** Changes made to your repository configuration only affect the selected repository. 
You can set option defaults globally in your in the **Edit \| Preferences \| Git Config** [settings](../Preferences/Commands.md#git-config).

## User

Configure your name and email address here - this is used to identify the author when new commits are created.

## Fetch and Pull

These settings allow you to configure 
- Whether to merge fetched changes, or to rebase the local branch onto the fetched changes, when pulling updates from a tracked remote branch.
- Whether to delete (prune) obsolete remote branches
- How to treat Submodules when pulling:
  - Always fetch new commits, tags, and branches from the submodule's remote
  - Update registered submodules
  - Initialize new submodules which have been added to the tracked remote branch

## Push

This configuration allows you to choose what happens when you attempt to push, and a referenced submodule which has changes.
- Abort - Your push operation will abort, and you will need to resolve the submodule synchronization, e.g. by pushing the submodule commit
- Ignore - Submodule changes will NOT be pushed to the remote. **Note**: If your changes depend on the changes you've made to your local submodule repository, other users may not be able to compile your changes.
- Push submodules first - SmartGit will automatically push changes to the Submodule, and then push the changes to your current repository.

## Signing

This allows you to configure the GPG program and your signing key to Sign Tags and Commits.
Please refer to [Signing](../../HowTos/Sign-Tags-and-Commits.md) for further information.

**Note**
> You need to ensure the specified GPG program is configured to use an agent that can ask you for your key's passphrase using a GUI.
> 
> Otherwise you may get a gpg error "cannot open tty \`/dev/tty': Device not configured".

## Encoding

Here you can also configure the text encoding SmartGit should assume when viewing or editing text files, e.g. with the Compare, Index Editor or Conflict Solver.

- UTF-8 with BOM, UTF-16 with Byte Order Markers (BOMs) are detected automatically.
- Files with UTF-8 and without BOMs are usually automatically detected from the content, so you don't usually need to explicitly add BOMs to UTF-8 encoded files.

## Tag-Grouping

Tag-Grouping specifies how tags (or more general: refs) will be grouped together.

This grouping:

-   allows a more compact display of a range of tags in the Log **Graph**
-   introduces additional "group"-nodes in the **Branches** view
-   adds **Closest Tags** category to the **Commit** view

For details on how tag-grouping patterns are specified, hover over the blue ![](../../images/icons/emoticons/information.png) markers.

# Other Options

SmartGit supports other options either in `<repository>/.git/config` or `~/.gitconfig`:

- `smartgit.gui.prefixAddBranch`: this value defines the default prefix in the **Branch \| Add Branch** dialog
- `smartgit.gui.prefixStartFeature`: this value defines the default prefix in the **Branch \| Git-Flow \| Start Feature** dialog
