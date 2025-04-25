# Git-LFS support in SmartGit

SmartGit provides support for common Git Large File Storage (Git-LFS) operations, allowing you to use LFS functionality such as LFS file tracking and locking, from the comfort of the SmartGit GUI.

Please refer to [Git LFS concepts](../GitConcepts/GitLargeFileStorage.md) for background, and benefits of using Git-LFS on selected files in your repository.

#### Tip
> 1. The Git LFS extension needs to be installed on your local computer, and LFS filters need to be enabled for a repository where LFS file storage will be used. 
> 2. It is recommended that you use the version of the Git executable that comes [bundled with SmartGit](../GUI/Preferences/Commands.md#git-executable), 
     and use SmartGit to enable and configure LFS with your repositories for best compatability.

## Enabling Git-LFS on a Git Repository with SmartGit

After selecting the required repository from the **Repository View**, use **Local \| LFS \| Install** to enable LFS support for your repository. 

SmartGit will prompt for confirmation. Select *OK* to confirm LFS support for the repository.

(This runs the equivalent `git lfs install` command in the repository.)

## Tracking a new file in LFS

After adding a new file under the Working Tree of your local repository, select the untracked file in the **Files View** and use the **LFS \| Track** command to track this file in LFS.

SmartGit will show a LFS Track dialog, prompting you to provide a tracking pattern:
- The default pattern will track just the selected file
- You can expand the pattern to include all files matching a pattern - use `*` as a wildcard, e.g. `*.png` will track all new files with a `.png` extension in LFS.

This is equivalent to running `git lfs track *.png` from the Git command line.

SmartGit will add the pattern into the `.gitattributes` file, which is used by identify files tracked by LFS.

#### Note
> Remember to add and commit the `.gitattributes` file into your Git repository!

## Locking LFS Files for Exclusive Editing
In order to prevent other users on a repository from concurrently editing a file tracked by LFS in your Git repository, 
you can [lock](../GitConcepts/GitLargeFileStorage.md#git-lfs-file-locking) a file on the LFS server to obtain exclusive modify access to the file.

#### Note
> 1. The ability to perform LFS locking is disabled by default in SmartGit.
>    To use LFS locking, you will need to toggle the [Low-Level Property](../GUI/AdvancedSettings/Low-Level-Properties.md) `status.lfs.locks` to `true` to enable the *Lock* command from SmartGit.
> 2. LFS file locking only makes sense once a repository and associated LFS files have been pushed to the remote server, where other users will contend for LFS files.
>    If no LFS server remote is detected by Git LFS, it will issue an error similar to `failed: missing protocol`

Once enabled, LFS Locking is available through the **LFS \| Lock** command from the **Files View** in all SmartGit Views:
- The **Files View** of the **Working Tree Window**
- The **Local Files** perspective of the **Standard Window**
- The **Files View** of the **Log Window**, provided that the Working Tree node of the commit Graph has been selected.

## Displaying locks

To see Git-LFS lock states in the **Files** views (both Log and Working tree window), *Git-LFS locks verification* must be enabled for your repositories. 

`git config 'lfs.https://github.com/<my_repo>.git/info/lfs.locksverify' true`



#### Technical Note on LFS Locks Verification

The locks verification configuration is stored in `git.config` with the section `[lfs "https://server/repo.git/info/lfs"]`, e.g.

```
[lfs "https://github.com/myrepo.git/info/lfs"]
    ...
    locksVerify = true
```

When locks verification is enabled, SmartGit will invoke the invoke additional commands:

- `git lfs locks --local`
- `git lfs locks --remote`

after every **Pull**, **Fetch** and after every background **Fetch** (if enabled in the **Preferences**, section **Background Commands**).

The output of these `git lfs locks` commands will be written to:

- `./git/smartgit/lfs-locks-local`
- `./git/smartgit/lfs-locks-remote`

Once these files are present, the **Name** column icon will start denoting the locking state for LFS files.

#### Example

The following screenshot shows how this display will look like:

- `file` is normal file to which no LFS lock information applies
- `huge` is *locked by someone else*
- `huge2` is *locked by yourself*
- `huge3` is *lockable* (configured in` .gitattributes`)

![](../attachments/53215476/53215477.png)

#### Note

> In the **Log** window, lock states will only be displayed for the **Working Tree** node.

## Troubleshooting

> 1. If the 'LFS \| Lock'  enable property `status.lfs.locks` in the **Preferences**, section **Low-level Properties**.
> 2. If your `git-lfs` executable is not found by SmartGit, try using absolute paths for the `git-lfs` executable configuration in the `gitconfig` file containing the Git-LFS filter definition.
>    Alternately, change your SmartGit Git executable configuration to to the bundled Git under the [Command Preferences](../GUI/Preferences/Commands#git-executable) options.
> 3. If you are encountering unexpected errors when invoking **Lock** or **Unlock** commands on files,
>    this may be caused by a strange behavior of current Git-LFS versions (2.5) which will fail when invoked with a working directory with an incorrect case.
>    To workaround the problem, make sure that the path in `repositories.xml` has correct case, especially the drive letter must be uppercase, for example:
>
> ``` java
> <obj type="@Repository" id="...">
>     <prop key="name" type="String" value="smartgit"/>
>     <prop key="favorite" type="boolean" value="true"/>
>     <prop key="git" type="boolean" value="true"/>
>     <prop key="path" type="String" value="D:\\smartgit"/>
>     <prop key="expanded" type="boolean" value="false"/>
> </obj>
> ```
