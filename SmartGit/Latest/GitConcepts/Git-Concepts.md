---
redirect_from:
  - /SmartGit/Latest/Git-Concepts
  - /SmartGit/Latest/Git-Concepts.html
---
# Git Concepts

This section aims to help you get started with Git and gives you an understanding of the fundamental concepts of the Git version control system.

## Distributed Version Control Systems

Unlike previous centralized version control systems such as Subversion (SVN), Visual Source Safe (VSS), or Concurrent Version Control (CVS), Git is a Distributed
Version Control System (DVCS).

Git has several advantages over classical centralized version control systems, such as:
- Users will get their own copy of a source repository (through a Cloning process) on their local computer, allowing version control even when offline.
- Commits can be created in the local repository and then Pushed to the remote repository when you are ready.
- Git has a streamlined mechanism for reviewing requests to bring new commits into an existing branch, called a Pull Request (PR).
- It is much easier to switch between branches in Git than with CVCS systems.

## Table of Common Terms used in Git

| Term  | Definition |
| ------------- | ------------- |
| Init  | (`git init`) is the command to create a new repository locally. You must connect to an empty remote repository to push changes in your local repository to the remote. |
| Clone  | Cloning (`git clone`) is the command used to create a local copy of an existing repository. |
| Pull Request  | A Pull Request (PR) is a request issued to merge changes made on one branch (e.g., changes made on a feature branch) into another branch (e.g., into a main or release branch). Pull Requests allow an ideal opportunity for code reviews |
| [Branch](Branches.md)  | A Branch is a named reference to a particular commit in a repository. When new commits are added to a branch, the branch will now point to the later commit. |
| Checkout | Checkout (`git checkout`) is the Git command to switch between or create new branches. |
| Staging | Staging is the process of identifying the files that have been changed (added, edited, or deleted) in your Working Tree and are to be included in the next commit. Git tracks staged files in the Git [index](The-Index.md). |
| [Commit](Commits.md) | Commits (`git commit`) is a unit or record of changes made to the files in a repository. A branch thus consists of a sequence of commits. |
| Local Repository | The local repository is a (clone of a) repository stored on your local system (in the `.git` folder). You should not make changes to the local repository directly. Instead, changing files in the Working Tree would be best. |
| Remote Repository | The repository from which your local repository copy has been cloned. The remote is often referred to as `origin` by convention. |
| Rebase | Rebasing (git rebase) provides an alternative to merging two branches by creating or appending equivalent commits representing the changes made in the source branch to the target branch. This removes the appearance of branching from the commit history. In visualization tools, rebased commits appear as a linear sequence of commits on the branch. |
| Squash Commits | Git allows creating a new, single, consolidated commit from a series of smaller commits, essentially the ‘rewriting’ history in a branch. This can be useful for removing an unnecessarily ‘noisy’ commit history from your repository; however, it has the downside of losing some of the audit trails of when and who made changes. |
| Merge (Commit) | A merge commit is a new commit added when two branches are merged. The log will retain information about both branches, and visualization tools will be able to show commits made on the divergent branches and where they branched off and merged. |
| Fast Forward | Fast forwarding is a technique Git uses to apply new commits to an existing branch by simply appending each commit to the branch in sequence. e.g., Fast forwarding can be used when `pulling` changes from a remote branch (if no local changes have been made), or when rebasing a branch from new commits held in a side branch. Fast forwarding has an advantage over squash and merge commits in that no new commits are needed. Fast forwarding cannot happen without new commits in both source and destination branches. |
| Cherry-Pick | Cherry picking (`git cherry-pick`) is an advanced feature that pulls a specific, existing commit into the current branch. Although cherry-picking can help pick specific features off side branches into a new release, extreme caution is needed to ensure all dependent commits are cherry-picked in sequentially. |
| [Working Tree](Working-Tree-States.md) | The working tree is the folder on your local system where you can change files in a repository and then stage and commit these changes. |
| Commit Hash | A Commit Hash (also known as a commit Id) is a unqiue SHA-1 hash of the contents of a commit, which will be invariably be unique (unless the commit data, including timestamps and metadata are all identical). |
| Bare Repository | A Bare Repository is a Git repository without a Working Tree. Usually, you will want a working directory, so Bare Repositories are generally only of interest to hosting providers like GitHub. |
| Secure Shell (SSH) | SSH is an encrypted network protocol historically used to authenticate and communicate between local and remote repositories.  **TODO** See SSH |
| HTTPS | HyperText Transfer Protocol Secure is an alternative protocol that Git can use to connect local and remote repositories.|
| Credential Manager | A Git Credential Manager is a secure tool that assists in retaining a user's credentials as required to access remote repositories. Credential Managers simply provide HTTPS access to remote repositories so that users aren't prompted for authentication on each git command.|
| Large File Storage | Git LFS is an extension that stores large binary files (BLOBs) separately from your repositories. This is useful because Git cannot track 'differences' between binary files in the same way it can with text files such as source code or wiki documents. Adding BLOBs directly to your Git repository can bloat the storage required and impact performance of commands between local and remote repositories.|
| [Submodules](Submodules.md) | Submodules allow a common repository (e.g., a library project) to be referenced by one or more 'parent' repositories. This enables the reuse of common code without maintaining separate copies of the common repository. |

**TODO** - Below still needs to be amended.

## Repository, Working Tree, Commit

First, we need to introduce some Git-specific terms which may have
different meanings in other version control systems such as Subversion.

Classical centralized version control systems such as Subversion (SVN)
have so-called \`working copies', each of which corresponds to exactly
one repository. SVN working copies can correspond to the entire
repository or just to parts of it. In Git, on the other hand, you always
deal with (local) repositories. Git's *working tree* is the directory
where you can edit files and it is part of a repository. So-called *bare
repositories*, used on servers as central repositories, don't have a
working tree.



#### Example
>
>
>
>Let's assume you have all your project-related files in a directory
>`D:\my-project`. Then this directory represents the repository, which
>consists of the working tree (containing all files to edit) and the
>attached repository meta data which is located in the
>`D:\my-project\.git` directory.
>
>

## Typical Project Life Cycle

As with all version control systems, there typically exists a central
repository containing the project files. To create a local repository,
you need to *clone* the *remote* central repository. Then the local
repository is connected to the remote repository, which, from the local
repository's point of view, is referred to as *origin*. The cloning step
is analogous to the initial SVN checkout for getting a local working
copy.

Having created the local repository containing all project files from
*origin*, you can now make changes to the files in the working tree and
*commit* these changes. They will be stored in your local repository
only, so you don't even need access to a remote repository when
committing. Later on, after you have committed a couple of changes, you
can [push them to the remote repository](Synchronizing-with-Remote-Repositories.md#push).
Other users who have their own clones of the origin repository can [pull from the remote repository](Synchronizing-with-Remote-Repositories.md#pull)
to get your pushed changes.
