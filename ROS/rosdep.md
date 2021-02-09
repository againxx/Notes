# Rosdep
rosdep is a command-line tool for installing system dependencies.

* `sudo rosdep init` initialize rosdep
* `rosdep update` update new added definitions (call without `sudo`)
* `rosdep check <package_name>` check if dependencies of package(s) have been met
* `rosdep install <package_name>` install dependency of a particular package
* `rosdep install --from-paths src --ignore-src -r -y` install dependency of all packages in the workspace
