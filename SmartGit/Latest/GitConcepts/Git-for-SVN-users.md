
#### Example
>
>
>
>Let's assume you have all your project-related files in a directory
>`D:\my-project`. This directory represents the repository, that
>consists of the working tree (containing all files to edit) and the
>attached repository meta data that is located in the
>`D:\my-project\.git` directory.
>
>

## Typical Project Life Cycle

As with all version control systems, a central repository typically contains the project files. 
You need to *clone* the *remote* central repository to create a local repository. Then, the local repository is connected to the remote repository, that, from the local repository’s point of view, is referred to as the *origin*. The cloning step is analogous to the initial SVN checkout for getting a local working copy.

Having created the local repository containing all project files from the *origin*, you can now make changes to the files in the working tree and *commit* these changes. They will only be stored in your local repository, so you don’t need access to a remote repository when committing. After you have committed a couple of changes, you can [push them to the remote repository](Synchronizing-with-Remote-Repositories.md#push). Other users with clones of the origin repository can [pull from the remote repository](Synchronizing-with-Remote-Repositories.md#pull) to get your pushed changes.
