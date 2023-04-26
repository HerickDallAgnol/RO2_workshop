# Tutorial Basico TurtleBot3
![Badge em Desenvolvimento](http://img.shields.io/static/v1?label=STATUS&message=EM%20DESENVOLVIMENTO&color=GREEN&style=for-the-badge)

## Instalação dos pacotes necessários:
  1. Gazebo
```
$ sudo apt-get install ros-foxy-gazebo-*
```
  2. Cartographer
```
$ sudo apt install ros-foxy-cartographer
$ sudo apt install ros-foxy-cartographer-ros
```
  3. Navigation2
```
$ sudo apt install ros-foxy-navigation2
$ sudo apt install ros-foxy-nav2-bringup
```
    
**Instalação dos pacotes do TurtleBot3:**

Deve estar dentro da pasta src

```
$ cd ~/dev_ws/src
$ sudo apt install ros-foxy-dynamixel-sdk
$ sudo apt install ros-foxy-turtlebot3-msgs
$ sudo apt install ros-foxy-turtlebot3
```
buildamos nossa workspace

```
$ cd ~/dev_ws
$ colcon build --symlink-install
$ source install/local_setup.sh
```

## Simulação no Gazebo

Primeiro devemos exportar o pacote de simulação do TurtleBot3:
```
$ cd ~/dev_ws/src
$ git clone -b foxy-devel https://github.com/ROBOTIS-GIT/turtlebot3_simulations.git
$ cd ~/dev_ws && colcon build --symlink-install
```
Iniciamos o TurtleBot3 World:
```
$ source install/local_setup.sh
$ export TURTLEBOT3_MODEL=waffle
$ ros2 launch turtlebot3_gazebo turtlebot3_world.launch.py
```

Em outro terminal, iniciamos o nodo de teleoperação:
```
$ source install/local_setup.sh
$ export TURTLEBOT3_MODEL=waffle
$ ros2 run turtlebot3_teleop teleop_keyboard
```




