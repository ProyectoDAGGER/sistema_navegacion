# Algoritmos de navegación 


## CERLAB UAV Autonomy Framework

Este framework fue desarrollado por el CERLAB del CMU. Desde 2021, este equipo ha trabajado en el Laboratorio de Ingeniería Computacional y Robótica (CERLAB) de la Universidad Carnegie Mellon. Esun equipo compuesto entre 5 y 15 estudiantes de posgrado, se enfoca en el desarrollo de algoritmos para abordar proyectos industriales reales utilizando su experiencia en tecnología UAV. Se especializan en tareas como inspección de túneles, mapeo de sitios de construcción e inspección de marcos de ventanas. Trabajan en estrecha colaboración con destacados socios industriales, como YKK AP Inc., Obayashi Corporation y TOPRISE CO., LTD, para proporcionar soluciones innovadoras que satisfagan las necesidades específicas de los clientes. Con un enfoque centrado en la tecnología y la innovación, el objetivo del equipo es desarrollar algoritmos avanzados que impulsen la eficiencia y la precisión en una variedad de aplicaciones industriales clave.
Ahora se explicará el proceso de instalación de este framework, primero se dan los requisitos de la máquina antes de la instalación del framework.

Ubuntu 18.04 ó Ubuntu 20.04.

ROS Noetic ó Melodic versión completa.
Paquetes de ROS como octomap, mavros y vision_msgs.
Framework de PX4-Autopilot.
Gazebo.
Una vez cumpliendo los requisitos mínimos, se procede a instalar las dependencias de ROS para nuestra máquina de ROS Noetic.

````
sudo apt install ros-noetic-octomap* && sudo apt install ros-noetic-mavros* 
sudo apt install ros-noetic-vision-msgs
````
Se crea el workspace para el repositorio.
````
mkdir ~/catkin_ws/src
cd ~/catkin_ws/src
git clone --recursive https://github.com/Zhefan-Xu/CERLAB-UAV-Autonomy.git
````
Se cambia a modo simulación (cuando se tenga un prototipo físico se omite este paso y se instala la versión para PX4)
````
cd catkin_ws/src/CERLAB-UAV-Autonomy/autonomous_flight
git checkout simulation
Ahora se crea el espacio de trabajo con catkin.
cd catkin_ws
catkin build
````
Ahora antes de inicializar cualquier simulación, se ejecuta el ejecutable de gazebo.
````
source catkin_ws/src/CERLAB-UAV-Autonomy/uav_simulator/gazeboSetup.bash
````
Se activa la rama de vuelo autónomo.
````
cd catkin_ws/src/CERLAB-UAV-Autonomy/autonomous_flight
git branch
git checkout simulation
cd ~/catkin_ws
catkin clean
catkin build
````
De esta manera queda activado el espacio de trabajo para simulaciones, para trabajar con PX4 y pruebas físicas se realiza lo siguiente:
````
cd catkin_ws/src/CERLAB-UAV-Autonomy/autonomous_flight
git branch
git checkout PX4
cd ~/catkin_ws
catkin clean
catkin build
````
## EGO PLANNER SWARM

Ego-Planner-Swarm es un avanzado planificador de enjambres de robots que integra el optimizador EGO (Mejora Esperada con Proceso Gaussiano) con tecnología para la generación de trayectorias topológicas implícitas, lo que resulta en una planificación y optimización de trayectorias eficientes en tiempo real. Este algoritmo es especialmente útil para abordar diversas tareas complejas que involucran grupos de robots, como manejo colaborativo, búsqueda y rescate, entre otras.
El enfoque fundamental de Ego-Planner-Swarm radica en la utilización inicial del optimizador EGO para generar un conjunto de trayectorias preliminares, seguido por el refinamiento y la mejora de estas trayectorias mediante la tecnología de generación de trayectorias topológicas implícitas. Durante este proceso de optimización, el algoritmo considera cuidadosamente las restricciones dinámicas, cinemáticas y ambientales de los robots para garantizar que las trayectorias resultantes sean factibles y efectivas en el entorno operativo.
Se observa el diagrama de flujo del sistema de navegación de los drones en un enjambre utilizando odometría visual-inercial (VIO):
![imagen de ](https://github.com/ProyectoDAGGER/Sistema_Navegacion/assets/163484218/ee80732c-583d-4902-9ba3-b0de88acfd1a)

Ahora se explicará el proceso de instalación de este framework, primero se dan los requisitos de la máquina antes de la instalación del framework.
Ubuntu 16.04, Ubuntu 18.04 y Ubuntu 20.04.

-ROS Noetic, Melodic ó Kinetic versión completa.
-Librería de ROS libarmadillo
-Framework de PX4-Autopilot.

Se instalan dependencias de ROS.
````
sudo apt-get install libarmadillo-dev
````
Se crea el espacio de trabajo y se clona el repositorio.
````
mkdir ego-planner-swarm/src
cd ego-planner-swarm/src
git clone https://github.com/ZJU-FAST-Lab/Swarm-Formation.git
````
Se crea el espacio con catkin (se usa -j1 si no se cuenta con muchos recursos en la máquina).
````
mkdir ego-planner-swarm/src
catkin build -j1
````
Si se quiere usar todos los recursos del dispositivo para simular el algoritmo, se procede a lo siguiente.
````
sudo apt install cpufrequtils
sudo cpufreq-set -g performance
````
Se instala ROSMON que permite la visualización en ROS de varios UAVs simultáneamente.
````
sudo apt install ros-noetic-rosmon
````
Antes de inicializar rosmon, se debe ejecutar ros de la raiz.
````
source /opt/ros/noetic/setup.bash
````
