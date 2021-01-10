# catkin_make & catkin_make_isolated

## History of catkin_make
### Why need catkin_make?
* In order to efficiently build numerous inter-dependent, but separately developed, CMake projects.
* ROS has a distributed development model with many modular projects.
* Catkin can merged numerous disparate projects so that they utilize a single target dependency tree and build space.
* A workspace’s source space contains boilerplate “top-level” CMakeLists.txt which automatically added all of the Catkin CMake projects below it
  to the single large CMake project

### Flaw of catkin_make
* Modification of one CMakeLists will reconfigure all other packages
* An error in leaf package (package with no dependencies) will prevent all packages from configuring
    - Packages might have colliding target names
    - One package defines variables needed by another one
    - Depend on order in which independent packages are built
* Requires developers to specify explicit dependencies on some targets inside of their dependencies
* It can only work on a homogeneous workspace consisting only of Catkin CMake packages.
    - Other types of packages like plain CMake packages and autotools packages cannot be integrated into a single configuration and a single build step

## History of catkin_make_isolated
### The improvement of catkin_make_isolated?
* Each package is independently configured, built and loaded into the environment
* This "atomic building" process can resolve
    - target collisions
    - target dependency management
    - other undesirable cross-talk between projects
    - heterogeneous automation of other buildtools plain CMake or autotools
* Other advantages
    - Allow building of part of the workspace
    - Build Catkin and non-Catkin projects into a single devel space
    - Build packages without re-configuring or re-building their dependencies
    - Remove the requirement that all packages in the workspace are free of CMake errors before any packages can be built

### Flaw of catkin_make_isolated
* Dramatically slower than `catkin_make` since it cannot parallelize the building of packages which do not depend on each other
* It also lacks robustness to changes in the list of packages in the workspace

## Latest version - caktin build
* Parallel version of catkin_make_isolated
* Build each packages in isolation and in topological order while parallelizing the building of packages that do not depend on each other

### Other improvements
* The use of sub-command “verbs” for better organization of build options and build-related functions
* Robustly adapting a build when packages are added to or removed from the source space
* Context-aware building of a given package based on the working directory
* The ability to completely clean a single package’s products from a workspace
* Utilization of persistent build metadata which catches common errors
* Support for different build “profiles” in a single workspace
* Explicit control of workspace chaining
* Additional error-checking for common environment configuration errors
* Numerous other command-line user-interface improvements
