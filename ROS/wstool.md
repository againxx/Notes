# wstool
* Command-line tools for maintaining a workspace of projects from multiple version-control systems based on a single workspace definition file (.rosinstall)
* Like a ROS version of `pip install -r`

## Relationship with Catkin
* Catkin workspaces create their own setup file and environment
* wstool is reduced to version control functions only
* The root directory of wstool workspace is the root of the catkin source directory (`catkin_ws/src`)

## Using wstool
* Initialize a workspace without a `rosinstall` file, this will initialize an empty workspace
    - `wstool init src`
* Initialize a workspace from a `rosinstall` file
    - `wstool init src PATH_TO_ROSINSTALL_FILE.rosinstall`
* Merge in additional `rosinstall` files
    - `wstool merge -t src PATH_TO_ROSINSTALL_FILE.rosinstall`
* Update the workspace, after you've created your workspace and added repositories
    - `wstool update -t src`
