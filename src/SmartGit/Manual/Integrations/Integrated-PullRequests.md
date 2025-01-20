# Integrated Pull Requests

When SmartGit detects changes on the hosting service, it will also refresh information on related Pull Requests from the hosting service:
- *Incoming* pull requests are those which other users have assigned to you for review and/or merging.
  These are displayed in a separate *Pull Requests* folder under the Branches view.
- *Outgoing* pull requests are those which you have initiated to other users/repositories, requesting them to pull your changes.
   These are displayed directly below the local (or if it does not exist), the remote branch in the *Branches View*.
- On the **Log Window**, the *Branches View* will show available Pull Requests - click to open a context menu to fetch the Pull Request

#### Incoming Pull Requests
When SmartGit detects an Incoming pull request assigned to you for merge or review, information about the Pull Request is retrieved from the hosting service and listed under the *Branches View* *Pull Requests* folder.
- To work with the pull request on the hosting providers web site, click on the Pull Request to open the context menu, and select *Open in Web Browser*
- To work with these pull requests locally in SmartGit (e.g. to review their commits, or Merge or Reject them), you first have to fetch them by invoking Fetch from the context menu of the pull request. 
  This will fetch all commits from the remote repository to a special branch in your local repository and will create an additional, virtual merge commit between the base commit from which the pull request has been forked and the latest (remote) pull request commit.
  This virtual merge commit is represented by a diamond icon in the Log Window.

When selecting this merge node in the Commits view, you can see the entire changes which a multi-commit pull request includes and you can comment on these changes, if necessary.

#### Commenting on Changes
Depending on the Hosting Service, comments can either be added to a commit, or to individual line changes on diffs in the commit.

**TODO** - Comments can be applied to a commit or to a Pull Request.

Pull Request Comments will be refreshed together with those pull requests which are locally available (see Fetch Pull Request above).
Plain Commit Comments will by default not be refreshed for performance reasons. To tell SmartGit to fetch plain commit comments, too, configure github.commitCommentPageLimit in the Preferences, Low-Level Properties.

Both, Pull Request and Plain Commit Comments, can refer either to a commit itself or to a specific line in a file:

Commit comments will show up in the Commits view.
Comments on individual lines will show up in the Changes view and the affected files will be highlighted in the Files and Commits view, too. This works the same way for line-comments of Pull Requests, provided that the pull request has been Fetched and the local pull request merge commit has been selected.
Comments can be created, modified and removed using the corresponding actions from the Comments menu or context menu actions in the Commits and Changes view. If a pull request merge commit is selected, only line-comments of the pull request can be manipulated.

More behavior of the GitHub integration can be customized by Low-Level Properties.


After commenting changes, it’s probably a good idea to Reject the pull request to signal the initiator of the pull request, that modifications are required before you are willing to pull his changes. If you are fine with a pull request, you may Merge it. This will request the GitHub server to merge the pull request and then SmartGit will pull the corresponding branch, so you will have the merged changes locally available.
