# Integrated Cloning

Once [integration](index.md) with a Hosting Provider has been configured, SmartGit's Clone command will allow navigation to browse repositories available to you on the hosting provider.
The required repository can then be selected and cloned, without needing to copy the Clone URL from the hosting provider and paste it into SmartGit.

SmartGit will display repositories on the Hosting Provider to which it has been granted access, including:
- *user* repositories
- *organization* (org) repositories

#### Example
> In the below diagram, the the SmartGit user has configured integrations to multiple Hosting Providers, and has selected the *Azure DevOps* icon.
> A list of repositories available to the user on Azure DevOps is is displayed beneath each organizational folder:

![Cloning a Repository using a connected Hosting Provider](../images/Integrations-Cloning.png)

*** TODO - MERGE FROM GITHUB

### Clone

When [cloning](../GUI/Repository/Clone.md) a repository, you now have the option of selecting your repository from a list, instead of entering a repository clone URL obtained from GitHub.
SmartGit will display your own (*user*) repositories, as well as repositories of your *organization(s)* (*org*).

![](../images/GitHubIntegration-Clone.png)

## Working Tree window

The Working tree window contains a light-weight GitHub integration which shows open incoming pull requests in the title of the **Branches** view.

#### Note

> Detailed pull request information and operations on pull requests are only available in the **Log** (see below).


## Log

In the *Log* window of your repository, you can interact with GitHub in following ways.
