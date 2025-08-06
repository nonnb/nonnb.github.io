# The Repositories View in SmartGit

The *Repositories View* shows a list of repositories known to SmartGit on the local computer, allowing you to open an existing repository, and shows you which repository(ies) are currently open by a **bold** highlight.

Please also refer to [Working with Repositories](Repository/index.md) for general Repository operations.

## Working with Repositories

SmartGit remembers repositories that you've previously opened and any GUI-related settings applied to each repository.
To open a repository, double-click it.
If the repository is already is open in another window, SmartGit will focus on that window.

If the current window is executing commands, or if **Open in New Window** has been selected from the repository's context menu, the repository will open in a new window.
To open multiple repositories simultaneously, select and highlight each repository (e.g., using **`Ctrl/Cmd` + click**) and choose **Open** from the context menu.

## Favorite Repositories
Repositories can be marked as favorites using the **Mark as Favorite** (**Unmark as Favorite**) option.
Favorite repositories are indicated with an asterisk (*) after the name and are sorted before non-favorite repositories.
Additionally, favorite repositories will receive background refresh operations.

## Grouping Repositories
Repositories can be arranged into *Group* folders in order to ease the management of large numbers of local repositories.

To create a group folder, right click in the **Repositories View** and select **Add Group**, or select **Add Group** from the **Repository** menu.

To move a repository into a group, right-click on the repository and select the target group, choose the **Move To** submenu and select the target folder.
Alternatively, you can select a repository and use drag-and-drop to move a repository inside a target group (see [autoscroll](Tips-and-Tricks.md#autoscrolling-while-drag-and-drop)).

#### Tips
> - Groups can be nested underneath other groups, by selecting the parent group and adding a new group.
> - You can move a nested group back to the top level by using **Move To** and then choosing *No Group*.
> - You can select multiple repositories by holding down *Control* or *Shift*.
> - To create a new top level repository, ensure no group folders or repositories are selected - you may need to hold Control to unselect a highlighted group.
