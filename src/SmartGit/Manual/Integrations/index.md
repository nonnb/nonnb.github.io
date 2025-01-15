# SmartGit Integrations with other Applications and Git Hosting Services

SmartGit works with most modern Git Hosting services, can integrate with several CI/CD tools, and can also be used with popular Issue Tracking systems. 
Please select one of the below topics for further information:

## Supported Git Hosting services:

Please refer to the applicable documentation in order to connect a SmartGit repository to a Git hosting provider:

- [Microsoft Azure DevOps](Azure-DevOps.md)
- [Atlassian Bitbucket Cloud](Bitbucket-integration) and [Bitbucket and Atlassian Stash On Premises](BitBucket-Server-Atlassian-Stash-integration.md)
- [GitHub](GitHub-integration) and [GitHub Enterprise On Premises](GitHub-Enterprise-Integration.md)
- [GitLab](GitLab.md)

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

### Visual Indicators and Navigation
The following visual indicators and productivity aids are made available once a repository is cloned from a linked hosting provider:
- An icon representing the hosting provider will appear above the *Branch View*. Clicking this icon will **TODO** seems to fetch ? Check for PRs and Comments?
- On the **Working Tree** window, a link will appear next to the icon above the *Branches View* which will show open Pull Requests (in the navigation view)




## Supported Continuous Integration / Continuous Deployment services:
- [GitHub Actions](GitHub-Actions)
- [Jenkins](Jenkins.md)
- [JetBrains TeamCity](TeamCity.md)

## Integration with other Software
- [Atlassian JIRA](JIRA.md) - Commit message extracted from JIRA ticket
- [Gerrit](Gerrit.md)
- [Git Large File Storage](Git-LFS.md)
