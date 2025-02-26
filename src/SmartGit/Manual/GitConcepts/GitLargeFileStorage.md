# Git Large File Storage (LFS)

Instead of committing large, or binary files directly into a repository, git can instead store these files in *Git Large File Storage*
This stores a pointer in the repository to the LFS file (CHECK)


- Need to install LFS locally (SmartGit can do this automatically)
- Remote Host must support LFS
- May be extra costs on the remote, or limits on the maximum file size (speculative)

Notes:
- Files don't need to be large to choose to store them in LFS. Since diffs

## Associating File Types with Git LFS
 
 `git lfs track "*.png"`
