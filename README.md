# WITMOTION-Standard-Modbus - Inclinómetro - Instalación para ROS Kinetic

## 1. Configurar la biblioteca de recursos
Dentro de Software & Updates, deben estar seleccionadas las opciones universe, restricted y multiverse.
## 2. Verificar variables de entorno
Se debe de asegurar de que las variables de entorno de ROS estén configuradas. Esto se verifica revisando las últimas líneas del archivo  `~/.bashrc` donde se debe encontrar escrito al final `source /opt/ros/kinetic/setup.bash` . De no ser así, esto se puede lograr escribiendo en el terminal echo `"source /opt/ros/kinetic/setup.bash" >> ~/.bashrc`.

Si se cuenta con varias distribuciones de ROS,  solo se debe de modificar el entorno shell actual y no se debe de predeterminar una versión de ROS por defecto en el terminal.

Para modificar solo el entorno shell actual, se debe de escribir en el terminal cada vez que se abra uno: `source /opt/ros/kinetic/setup.bash`

## 2. Instalar rosinstall
Se debe de verificar que estén instalados los paquetes: `python-rosinstall` y `python-rosinstall python-rosinstall-generator python-wstool build-essential`

Estos paquetes se instalan con las siguientes instrucciones:

    sudo apt-get install python-rosinstall
    sudo apt-get install python-rosinstall python-rosinstall-generator python-wstool build-essential
    
## 3. Instalación de dependencias de ROS IMU

    sudo apt-get install ros-kinetic-imu-tools ros-kinetic-rviz-imu-plugin
    sudo apt-get install python-visual

## 4. Instalación del pip

    curl https://bootstrap.pypa.io/pip/2.7/get-pip.py --output get-pip.py
    sudo python2 get-pip.py

## 5. Instación de dependencias

    pip install modbus_tk

## 2.2 Crear espacio de trabajo


	   cd ~/ 
	   git clone https://github.com/davidrdcr/wit.git
    	   cd ~/wit/wit_ros_ws/
	   catkin_make
	   cd ~/wit/wit_ros_ws/src/scripts/
	   sudo chmod 777 *.py
	   echo "source ~/wit/wit_ros_ws/devel/setup.sh" >> ~/.bashrc
	   source ~/.bashrc

## 6. Controlador y visualización de ROS
Verifique el número del puerto USB. No conecte el USB de la IMU primero. Ingrese `ls /dev/ttyUSB*` en el terminal y vea los dispositivos existentes. Luego inserte el USB en la computadora e ingrese `ls /dev/ttyUSB*` en el terminal para detectar el dispositivo ttyUSB adicional.

## 7. Configure el puerto
Otorgue los derechos de administrador del puerto serie correspondiente. Cada vez que vuelva a insertar el puerto USB, deberá volver a otorgar derechos de administrador al puerto serie.

    sudo chmod 777 /dev/ttyUSB0

## 8. Ejecute del archivo de inicio

    roslaunch wit_ros_imu display_and_imu.launch

## 9. Lea los datos
Abra tres nuevas terminales e ingrese las siguientes líneas de comando.

    rostopic echo /wit/imu
    rostopic echo /wit/mag
    rostopic echo /wit/location

## 10. Descripción de los documentos relevantes

 - display_and_imu.launch, abre el nodo del controlador IMU y el modelo visual escrito en visual. (solo es compatible con ubuntu 16.04)
 - wit_imu.launch, abre el nodo controlado por IMU.
 - rviz_and_imu.launch, abre el nodo del controlador IMU y la visualización de Rviz.

## 11. Instale cutecom

    sudo apt-get install cutecom -y

## 12.  Otorgue permisos de lectura y escritura.

    sudo chmod 777 /dev/ttyUSB0 

## 13. Verifique los datos
Ingrese cutecom en la terminal. Si puede encontrar información que comience con `55 51`, `55 52`, `55 53`, entonces no hay problema con los datos enviados por el módulo. Si hay datos pero no se encuentran los datos de encabezado correctos, debe verificar el valor en baudios, la configuración de velocidad en baudios, cambie a la velocidad en baudios correcta y se mostrará.
