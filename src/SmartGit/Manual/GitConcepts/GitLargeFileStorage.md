# Git Large File Storage (LFS)

# Git LFS

Git Large File Storage (LFS) is an optional addition to the Git standard, to allow storage of specific types of files (typically large or binary files) on a designated LFS Server, instead of on a Git Server.
Once a file has been marked for tracking by LFS, the committed file will be replaced by a 'pointer' file in the Git Repository.
The file is stored using a Content Addressable Storage schema, which computes the SHA-256 hash of the uploaded file which is used to identify the file's identity.

Git LFS works by applying LFS's `smudge` and `clean` filter commands on files which have been marked for LFS tracking in the `.gitattributes` configuration file.
- the `smudge` filter to retrieve the actual LFS file and replace the file pointer in your working directory.
- conversely, when checking in a file which has been added to LFS tracking, Git will apply the `clean` filter which will substitute the file with a SHA file location.

The `.gitattributes` should also be added into the repository, so that all collaborators can retrieve and work with files which have been tracked by LFS.

Git LFS offers a `lock` option on files, which provides a pessimistic (or reserved) checkout mechanism so that a user can exclusively modify a LFS file.
When a LFS tracked file is checked in, it will obtain a new SHA file location, and the pointer file will be updated to reflect the new file version's location.

## Benefits
- The main Git repository will be leaner without large binary files, so operations such as cloning are greatly reduced.
- Collaborators can opt to 

There are some other considerations when working with LFS, such as:
- If your repository already has files that you wish to move from Git to LFS, you may need to use git tools such as `git-filter-repo` to permanently remove these files from a repository,
  by rewriting the commit history.
- If a collaborator to your LFS-enabled repository does not have the Git LFS client installed, when cloning they will see the pointer files instead of the actual file.

As a result, it is advisable to set your Git LFS strategy when your repsitory is first created.

SmartGit [automatically handles](../Integrations/Git-LFS.md) much of the complexity of installing and managing LFS interactions, when connecting to repositories with Git LFS servers.

.gitattributes

****************



Instead of committing large, or binary files directly into a repository, git can instead store these files on a *Large File Storage* (LFS) server.
This stores a pointer in the repository to the LFS file (CHECK)


- Need to install LFS locally (SmartGit can do this automatically)
- Remote Host must support LFS
- May be extra costs on the remote, or limits on the maximum file size (speculative)

Notes:
- Files don't need to be large to choose to store them in LFS. Since diffs

## Associating File Types with Git LFS
 
 `git lfs track "*.png"`


.gitattributes file

It is recommended that the `.gitattributes` file be committed, as this will assist other contributors to the repository

SmartGit does this by default (TBC)
