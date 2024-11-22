## Stashing

Stashes are a convenient way to put the current working tree changes or just some selected files aside and re-apply them later.

Use **Local \| Stash All** to stash away all local modifications of your working tree. To stash away only the selected files, use **Local \| Stash Selection**. The resulting stash will show up in the **Branches** view.

#### Note

>
>The option **Include untracked files** (Preferences, page **Commands**)
> is convenient to include *untracked* files for the stash as well.
> Depending on the operating system it may take significantly longer to execute the operation.
>

Right-click the stash and select **Apply Stash** to re-apply the contained changes to your Working Tree (e.g. after switching branches). To get rid of obsolete stashes, use **Drop Stash**, however be aware that this will irretrievably get rid of the changes which are stored in the stash. The **Rename Stash** command allows you to change the displayed stash message.
