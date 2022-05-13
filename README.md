# weed_robot_description

Description of the weeding robot in URDF format using xacro.

The [urdf](urdf) folder contains the xacro files of the robot description. The following command can be used to generate the URDF file:
```
$ xacro urdf/weed_robot.xacro > weed_robot.urdf
```

The configuration file [config/weed_robot.yaml](config/weed_robot.yaml) specifies the mass and dimensions of each part of the robot. 
With this information, the moment of inertia matrix is calculated for each part.
Additionally, the coefficients kp (*contact stiffness*), kd (*damping*) and mu (*friction coefficients*) for the robot wheels are specified.

The [meshes](meshes) folder contains 3D meshes in STL format.
Those with the *heavy* suffix have higher definition.
By default, the ones without this suffix are used.
For the solar panels part there is a mesh in COLLADA format [meshes/panels.dae](meshes/panels.dae) that adds texture.

The [rviz](rviz) folder contains different RViz configurations for viewing the robot from different angles.

![Screenshot](img/rviz.png)

To visualize the robot model with RViz use [launch/rviz.launch](launch/rviz.launch) with the following arguments:
* meshes
  * true: generates the URDF file using STL and DAE meshes for the visual model and simple geometric shapes for the collision model.
  * false: generates the URDF file using simple geometric shapes for both the visual and collision models (useful to verify the collision model).
* config: this parameter indicates the configuration file for rviz (by default it uses *normal*, but you can configure *bottom* and *top* for other views).

For example:
```
$ roslaunch launch/rviz.launch meshes:=true config:=normal
```