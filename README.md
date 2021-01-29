# weed_robot_description

Descripción del robot desmalezador en formato URDF usando xacro.

En la carpeta [urdf](urdf) se encuentran los archivos xacro de la descripción del robot. Para generar el archivo URDF se puede usar el comando:
```
$ xacro urdf/weed_robot.xacro > weed_robot.urdf
```

El archivo de configuración [config/weed_robot.yaml](config/weed_robot.yaml) especifica la masa y las dimensiones de cada parte del robot. 
Con dicha información se calcula la matriz de momento de inercia para cada parte.
Adicionalmente, se especifican los coeficientes kp (*contact stiffness*), kd (*damping*) y mu (*friction coefficients*) para las ruedas del robot.

En el directorio [meshes](meshes) se encuentran las mallas 3D en formato STL.
Las que tienen el sufijo *heavy* tienen mayor definición.
Por defecto, se utilizan las que no tienen dicho sufijo.
Para la parte de los paneles solares existe una malla en formato COLLADA [meshes/panels.dae](meshes/panels.dae) que le agrega textura.

La carpeta [rviz](rviz) contiene distintas configuraciones de RViz para visualizar al robot desde diferentes ángulos.

![Screenshot](img/rviz.png)

Para visualizar el modelo del robot con RViz usar [launch/rviz.launch](launch/rviz.launch) con los siguientes argumentos:
* meshes
  * true: genera el archivo URDF usando las mallas STL y DAE para el modelo visual y figuras geométricas simples para el modelo de colisión.
  * false: genera el archivo URDF usando formas geométricas simples tanto para el modelo visual como para el de colisión (útil para verificar el modelo de colisión).
* config: este parámetro indica el archivo de configuración para rviz (por defecto usa *normal*, pero se puede configurar *bottom* y *top* para otros puntos de vista).

Ejemplo:
```
$ roslaunch launch/rviz.launch meshes:=true config:=normal
```