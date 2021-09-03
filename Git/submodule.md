# Submodule

## Gitlink
> A _gitlink_ is a link from _tree object_ to a _commit object_

* Normally, every commit object has a link to a tree object that specifies current snapshot
* However, git also use the gitlink mechanism to indicate a direction reference to another repository
* When using `git ls-tree HEAD` gitlink will be of type *commit* and has mode 160000
* Git usually treats gitlinks as simple pointer values or references to other repositories, and will not dereference the gitlinks for most operations
* So gitlinks link to objects that are allowed to be **missing** from your repository

## Rationale
Two use cases:
* Using another project while maintaining **independent** history, the superproject has its own freedom to pin to a particular version of subproject
* Splitting a project into multiple repositories and tying them back together, which can overcome some git drawbacks
    - Scale poorly for large repositories containing content that is not compressed by delta computation between trees (large binary assets)
    - Require the whole working tree present, it does not allow partial trees to be transferred in fetch or clone
    - Cannot implement read/write policies for different users

From the gitlink's perspective, Its jobs is simple:
* Follow the gitlinks and checkout the corresponding repositories for you

## Add
Git submodule command needs to know where to checkout the repository for you
* `git submodule add <git_repo> <dir>`
* After adding submodule, there will be a **.gitmodules** under git root directory
* And git will also clone the submodule repo at the given directory

## Init / Deinit
Next, we need to copy the settings from the **.gitmodules** file into **.git/config** file, that we can edit freely.
The reason for this step is that you can reconfigure your local submodules to point at a different repository from the official one in **.gitmodules**
* `git submodule init`
* `git submodule deinit` will empty the working directory and modifies the superproject's **.git/config** file, but leave the superproject's history untouched

