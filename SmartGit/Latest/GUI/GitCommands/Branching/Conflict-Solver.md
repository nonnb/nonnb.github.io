# Using the SmartGit Conflict Solver to resolve merge conflicts

SmartGit comes with a Conflict Solver tool which allows merge conflict resolution using a standard Three Way merge approach.

- The **left pane** shows the local branch commit version of the file (`ours`)
- The **center pane** shows the current conflicted Working Tree version of the file, including the merge confict markers. 
  You can use the `Base Changes` command to view the original version of the file (Common Base)
- The **right pane** shows the merge source version of the file (`theirs`)

TODO - Image [Tools-SmartGit-ConflictSolver.png]

The following commands are available in the SmartGit conflict resolver (commands are available as buttons, and in the Drop Down menu):
- **Base Changes** - opens a window which shows the original Common Base version of the file (:1) instead of the current Working Tree file (i.e. shows the original version before either `ours` or `theirs` changes were made to the file). 
- **Save** - This will save any changes made to the working tree file (even if there are still conflict markers present)
- **Prev Change** - Moves the cursor to the previous change in the selected pane.
- **Next Change** - Moves the cursor to the next change in the selected pane.
- **Take Left, Right** - Replaces the conflict with both left and right changes, firstly `our` change then `their` change (command is only available in the Working Tree pane)
- **Take Left** - Replaces the conflict with only the left (`our`) change and discards the right (`their`) change (command is only available in the Left + Working Tree panes)
- **Take Right** - Replaces the conflict with only the right (`their`) change and discards the left (`our`) change (command is only available in the Working Tree + Right panes)
- **Take Right, Left** - Replaces the conflict with both left and right changes, firstly `their` change, then `our` change (command is only available in the Working Tree pane)
- **Left + Marge** - This hides the right (`theirs`) window pane
- **All** - This shows all three panes (`ours`, `working tree`, and `theirs`)
- **Right + Merge** - This hides the left (`ours`) window pane.
- **Merge Below** - This moves the `working tree` pane to the bottom - this is useful for merging files with long lines.
- **Close** - Closes the Conflict Solver. If you haven't saved changes, you will be prompted to do so. The Conflict Solver will warn you if there are any unresolved conflicts remaining in the Working tree file.

If you have a preference for another 3 way merge tool for resolving merge conflicts, you can substitute the SmartGit Conflict Solver with another standalone tool.
TODO link Refer to [Preferences | Tools](../../Preferences/Tools.md) for instructions on how to switch to another Conflict Resolver tool.
