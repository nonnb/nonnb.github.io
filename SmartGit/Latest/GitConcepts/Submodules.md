# Git Submodules

Often, software projects within your organization are not completely self-contained, but share
common components with other software projects. Git offers a feature called
*submodules*, which allows you to embed one Git repository into another.

Submodules are especially useful when your organization does not use a Package Management server (such as Maven, npm or NuGet), 
but instead requires dependency projects to be embedded or re-built within your solutions.

A submodule is a nested repository that is embedded in a dedicated
subdirectory of the working tree (which belongs to the parent
repository). A submodule always references a specific commit of
the embedded repository. The definition of the submodule is stored as a
separate entry in the parent repository's git object database.

The link between working tree entry and foreign repository is stored in
the `.gitmodules` file of the parent repository. The `.gitmodules` file
is usually versioned, so it can be maintained by all users and/or
changes are propagated to all users.

Setting submodule repositories involves an initialization process, in
which the required entries are added to the `.git/config` file. The user
may later adjust it, for example to fix SSH login names.

Please refer to [Submodules in SmartGit](../Submodules) to see how to work with Submodules inside SmartGit.
