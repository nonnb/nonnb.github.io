# Integrated Comments (Log View Only)

Once [integrated with a Hosting Provider](index.md), SmartGit allows comments on commits and pull requests in the repository to be retrieved from the Hosting Provider.

The [**Log Window**](../GUI/Log-Window.md) provides an additional *Comments* tab at the top right hand side of the **Files View**.

Selecting a comment allows you to:
  - *Jump To* the comment, by showing the comment at the applicable location in the reviewed file in the **Compare View**.
  - *Edit* or *Delete* a comment (if the comment was created by yourself)
  - *Reply To* the comment. SmartGit will prompt you for a reply message.

Pull Request Comments will be refreshed together with those pull requests which are locally available (see Fetch Pull Request above).
Plain Commit Comments will by default not be refreshed for performance reasons.
To tell SmartGit to fetch plain commit comments, too, configure option `github.commitCommentPageLimit` in [**Preferences \| Low-Level Properties**](../GUI/AdvancedSettings/Low-Level-Properties.md)

Both, Pull Request and Plain Commit Comments, can refer either to a commit itself or to a specific line in a file:

Comments on individual lines will show up in the Changes view and the affected files will be highlighted in the Files and Commits view, too. 
This works the same way for line-comments of Pull Requests, provided that the pull request has been Fetched and the local pull request merge commit has been selected.
Comments can be created, modified and removed using the corresponding actions from the Comments menu or context menu actions in the Commits and Changes view. 
If a pull request merge commit is selected, only line-comments of the pull request can be manipulated.

After commenting changes, it’s probably a good idea to Reject the pull request to signal the initiator of the pull request, that modifications are required before you are willing to pull his changes. If you are fine with a pull request, you may Merge it. This will request the GitHub server to merge the pull request and then SmartGit will pull the corresponding branch, so you will have the merged changes locally available.

*** TODO - MERGED FROM GITHUB

### Comments

GitHub allows to comment on a commit itself or individual line changes (*diffs*). Comments can be applied to a commit or to a Pull Request. Pull Request Comments will be refreshed together with those pull requests which are locally available (see **Fetch Pull Request** above). Plain Commit Comments will by default not be refreshed for performance reasons. To tell SmartGit to fetch plain commit comments, too, configure `github.commitCommentPageLimit` in the **Preferences, Low-Level Properties**.

Both, Pull Request and Plain Commit Comments, can refer either to a commit itself or to a specific line in a file:

- Commit comments will show up in the **Commits** view.
- Comments on individual lines will show up in the **Changes** view and the affected files will be highlighted in the **Files** and **Commits** view, too. This works the same way for line-comments of Pull Requests, provided that the pull request has been **Fetch**ed and the local pull request *merge* commit has been selected.

Comments can be created, modified and removed using the corresponding actions from the **Comments** menu or context menu actions in the **Commits** and **Changes** view. If a pull request *merge* commit is selected, only line-comments of the pull request can be manipulated.

More behavior of the GitHub integration can be customized by [Low-Level Properties](../GUI/Preferences/index.md).


**TODO** - Comments can be applied to a commit or to a Pull Request.
Depending on the Hosting Service, comments can either be added to a commit, or to individual line changes on diffs in the commit.
