# SDF

SDF = Simulation Description Format was created for use in Gazebo to solve the shortcomings of URDF

## Shortcomings of URDF
* Can only specify kinematic and dynamic properties of a single robot
* Cannot specify the pose of the robot itself within a world
* Cannot specify joint loops (parallel linkages)
* Lacks friction and other properties
* Cannot specify things that are not robots such as lights, heightmaps, etc.
* The URDF syntax breaks the proper formatting with heavy use of XML attributes, which in turn makes URDF more inflexible

## Virtue of SDF
* Complete description for everything from the world level down to the robot level
* Scalable, makes it easy to add and modify elements
