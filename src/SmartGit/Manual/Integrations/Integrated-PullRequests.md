# Integrated Pull Requests

If a repository has been cloned from an [integrated Hosting Provider](index.md), when SmartGit detects changes on the hosting service, 
it will also refresh information on related Pull Requests (PRs) from the hosting service.

- In the **Standard Window**, clicking on the Hosting Provider icon will check for new branches and Pull Requests on the remote.
  If open PR's are present, a hyperlink will be shown taking you to the PR on the *Branches View* of the **Log Window**
- On the **Log Window**, the *Branches View* will show available Pull Requests - you can click on the Hosting Provider Icon to refresh available *Pull Requests* on the remote.

![Pull Requests under the Log Window Branches View](../images/Integrations-Branches-PullRequests.png)
  
  - To work with the PR on the Hosting Provider web site, click on the Pull Request to open the context menu, and select *Open in Web Browser*
  - To work with these pull requests locally in SmartGit (e.g. to review their commits, or Merge or Reject them), the commits in the PR can be fetched by invoking *Fetch* from the context menu of the pull request. 
  This will fetch all commits from the remote repository to a special branch in your local repository and will create an additional, virtual merge commit between the base commit from which the pull request has been forked and the latest (remote) pull request commit.
  The virtual merge commit is represented by a diamond icon in the *Graph View* of the **Log Window**.

![Pull Requests under the Log Window Branches View](../images/Integrations-PullRequest-VirtualMergeCommit.png)


## Additional Functionality (Currently Available on GitHub only)

- *Incoming* pull requests are those which other users have assigned to you for review and/or merging.
  These are displayed in a separate *Pull Requests* folder under the Branches view.
- *Outgoing* pull requests are those which you have initiated to other users/repositories, requesting them to pull your changes.
   These are displayed directly below the local (or if it does not exist), the remote branch in the *Branches View*.


#### Incoming Pull Requests
When SmartGit detects an Incoming pull request assigned to you for merge or review

When selecting this merge node in the Commits view, you can see the entire changes which a multi-commit pull request includes and you can comment on these changes, if necessary.

