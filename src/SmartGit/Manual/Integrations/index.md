# SmartGit Integrations with other Applications and Git Hosting Services

SmartGit works with many modern Git Hosting services, and can also be used with popular Issue Tracking systems. 
These integrations allow extended functionality in SmartGit, which can improve productivity within a team as part of a larger Software Engineering development process (often referred to as 'Dev Ops' processes)

## Supported Git Hosting services:

Please refer to the applicable vendor specific documentation in order to connect a SmartGit repository to a Git hosting provider:

- [Microsoft Azure DevOps](Azure-DevOps.md)
- [Atlassian Bitbucket Cloud](Bitbucket-integration) and [Bitbucket and Atlassian Stash On Premises](BitBucket-Server-Atlassian-Stash-integration.md)
- [GitHub](GitHub-integration) and [GitHub Enterprise On Premises](GitHub-Enterprise-Integration.md)
- [GitLab](GitLab.md)

**TODO Show icons for each vendor **

#### Note on Terminology:

> The terminology between hosting providers differs somewhat for equivalent or similar features, as per the below table.
> SmartGit will automatically change terminology to adapt to the Hosting Provider connected to the repository, where applicable.
> However, for brevity, the online documentation will use the GitHub terminology when referencing features linked to online hosting providers.

| GitHub             | Azure DevOps | BitBucket    | GitLab          |
| ------------------ | ------------ |------------- | --------------- |
| Pull Request       | Pull Request | Pull Request | Merge Request   |
| Reject PR          | Abandon PR   | Decline PR   | Close PR        |
| Approve PR Changes |              | Approve      |                 |
| *                  |              | Unapprove    | Revoke Approval |


### Feature Support Matrix:

|                                       | GitHub | Azure DevOps | BitBucket | GitLab    |
| ------------------------------------- | ------ | ------------ |---------- |---------- |
| Navigation Links                      |   Yes  |      *       |     *     |     *     |
| Repo Select + Clone                   |   Yes  |     Yes      |     Yes   |     Yes   |
| Inbound and Outbound PR Notifications |   Yes  |     Yes      |     Yes   |     *     |
| Initiate Pull Request                 |   Yes  |     Yes      |     Yes   |     Yes   |
| View, Add, Edit and Delete Comments   |   Yes  |     Yes      |     Yes   |     Yes   |
| Approve Pull Request                  |   Yes  |     Yes      |     Yes   |     Yes   |
| Merge Pull Request                    |   Yes  |     Yes      |     Yes   |     Yes   |
| Close Pull Request                    |   Yes  |     Yes      |     Yes   |     Yes   |

### Cloning

Once integration with a hosting provider has been configured, instead of pasting the remote Clone Url into SmartGit, instead, SmartGit will allow navigating to the hosting provider and showing available repositories, 
where a repository can be selected and cloned locally.

SmartGit will display your own (*user*) repositories, as well as repositories of your organization (*org*).

**TODO Icon**

### Visual Indicators and Navigation
The following visual indicators and productivity aids are made available once a repository is cloned from a linked hosting provider:
- An icon representing the hosting provider will appear above the *Branch View*. Clicking this icon will **TODO** seems to fetch ? Check for PRs and Comments?
- On the **Working Tree Window**, a link will appear next to the icon above the *Branches View* which will show open Pull Requests (in the navigation view)
- On the **Log Window**, the *Branches View* will show available Pull Requests on the remote repository on the hosting provider.
- In the **Standard Window**, 

### Pull Request functionality

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



## Supported Continuous Integration / Continuous Deployment services:
- [GitHub Actions](GitHub-Actions)
- [Jenkins](Jenkins.md)
- [JetBrains TeamCity](TeamCity.md)

### Additional SmartGit Features
- A `CI` indicator is shown in the *All Branches + Tags* tab of the **Standard Window** on the branch(es) which have been configured for CI Pipelines
- A branch marked witht the `CI` indicator can be clicked to open a context menu, allowing navigation to the latest CI Result on the CI/CD service provider

## Integration with other Software
- [Atlassian JIRA](JIRA.md) - Allows commit messages to be extracted from an open JIRA ticket
- [Gerrit](Gerrit.md) - **TODO**
- [Git Large File Storage](Git-LFS.md)
