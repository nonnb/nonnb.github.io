# Git Large File Storage (LFS)

# Git LFS

Git Large File Storage (LFS) is an optional addition to the Git standard, to allow storage of specific types of files (typically large or binary files) on a designated LFS Server, instead of on a Git Server.
Once a file has been marked for tracking by LFS, the committed file will be replaced by a 'pointer' file in the Git Repository.
The file is stored using a Content Addressable S

Git LFS works by applying smudge and clean filter commands on files identified for LFS tracking in a `.gitattributes` configuration file.

The `.gitattributes` should also be added into the repository, so that all collaborators can retrieve files using LFS.

## Benefits
- The main Git repository will be leaner without large binary files, so operations such as cloning are greatly reduced.
- Collaborators can opt to 

There are some other considerations when working with LFS, such as:
- If your repository already has files that you wish to move from Git to LFS, you may need to use git tools such as `git-filter-repo` to permanently remove these files from a repository,
  by rewriting the commit history.
- If a collaborator to your LFS-enabled repository does not have the Git LFS client installed, when cloning they will see the pointer files instead of the actual file.

As a result, it is advisable to set your Git LFS strategy when your repsitory is first created.

SmartGit [automatically handles](../Integrations/GitLargeFileStorage) much of the complexity of installing and managing LFS interactions, when connecting to repositories with Git LFS servers.

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
