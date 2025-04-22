# Git Large File Storage (LFS)

# Git LFS

Git Large File Storage (LFS) is an optional addition to the Git standard, to allow storage of specific types of files (typically large, or binary files) on a designated LFS Server, instead of within the Git Repository.
Once a file has been marked for tracking by LFS, the committed file will be replaced by a 'pointer' file in the Git Repository.

However, when working locally, if a Git-LFS aware client has been installed, files stored in LFS will be downloaded and will replace the pointer files in the [Working Tree](), providing a seamless user experience.

LFS files are stored using a Content-Addressable Storage schema, which computes the SHA-256 hash of the uploaded file which is used to identify the file's identity.

Git LFS works by applying LFS's `smudge` and `clean` filter commands on files which have been marked for LFS tracking in the `.gitattributes` configuration file.
- when cloning or fetching, the `smudge` filter is used to retrieve the actual LFS file and replace the file pointer in your working directory with the file retrieved from LFS.
- conversely, when checking in a file which has been added to LFS tracking, Git will apply the `clean` filter which will substitute the file with a SHA file location.

When working with LFS, a `.gitattributes` file is created, which tracks which files are being tracked in LFS.
The `.gitattributes` file should also be added into the repository, so that all collaborators can retrieve and work with files which have been tracked by LFS in a consistent manner.

Git LFS offers a `lock` option on files, which provides a pessimistic (or reserved) checkout mechanism so that a user can exclusively modify a LFS file.
When a LFS tracked file is checked in, it will obtain a new SHA file location, and the pointer file will be updated to reflect the new file version's location.

## Benefits
- The main Git repository will be leaner without large binary files, so operations such as cloning are greatly reduced.
- Collaborators can opt to ignore LFS files when cloning, if they do not need to work with LFS files, in which case they will see the pointer files in their local Working Tree.
- Users or CI/CD pipelines which do not need files stored in LFS won't require the additional disk space otherwise required of the files stored in LFS.

There are some other considerations when working with LFS, such as:
- If your repository already has files that you wish to move from Git to LFS, you may need to use git tools such as `git-filter-repo` to permanently remove these files from a repository,
  by rewriting the commit history.
- If a collaborator to your LFS-enabled repository does not have the Git LFS client installed, when cloning they will see the pointer files instead of the actual file.

As a result, it is advisable to set your Git LFS strategy when your repsitory is first created, especially if you know that large binary files will be used in the project.

## Common LFS commands

SmartGit [automatically handles](../Integrations/Git-LFS.md) much of the complexity of installing and managing LFS interactions, when connecting to repositories with Git LFS servers.

The below command line options may be useful if you prefer manual interaction or want to see the equivalent SmartGit behaviour:

### Installing the LFS client on a local computer:

`git lfs install`

*SmartGit command*: **Local \| LFS \| Install**

### Add specific file types to LFS

The below will automatically replace existing, and store new `.png` files in LFS, and replace `.png` files with a pointer file when new commits are added to your Git repository:
 
 `git lfs track "*.png"`

 *SmartGit command*: Select an untracked file in the **Files View** and invoke **Local \| LFS \| Track**. SmartGit will detect and suggest a matching pattern for the selected file, which you can adjust if necessary.

### The .gitattributes File

As soon as any files have been tracked in LFS, a `.gitattribute` file will be created in the root of the Working Tree directory.
Remember to add `.gitattributes` to your repository:

`git add .gitattributes`

#### Note:
> Is is recommended that you do not manually edit the `.gitattributes` file.
> Instead, either use SmartGit's File View, or `git lfs track` shortcuts to add or remove files from LFS.
