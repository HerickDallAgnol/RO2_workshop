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

```
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
Deve haver as seguintes pastas dentro da src:

![image](https://user-images.githubusercontent.com/112727443/235183551-3fbb8788-05f6-4093-8a34-e4fdafcf01e2.png)


Iniciamos o TurtleBot3 World:
```
$ source install/local_setup.sh
$ export TURTLEBOT3_MODEL=waffle
$ ros2 launch turtlebot3_gazebo turtlebot3_world.launch.py
```
![image](https://user-images.githubusercontent.com/112727443/235184446-1260b552-5931-402b-b8af-4817207233e9.png)

Em outro terminal, iniciamos o nodo de teleoperação:
```
$ source install/local_setup.sh
$ export TURTLEBOT3_MODEL=waffle
$ ros2 run turtlebot3_teleop teleop_keyboard
```
![image](https://user-images.githubusercontent.com/112727443/235184988-517ccd64-b0e9-4379-aa40-9e1a3fdabee4.png)

# Simulação SLAM 

O SLAM (Simultaneous Localization and Mapping) é uma técnica para desenhar um mapa estimando a localização atual em um espaço arbitrário.

## Mapeamento

Iniciamos o TurtleBot3 World:
```
$ source install/local_setup.sh
$ export TURTLEBOT3_MODEL=waffle
$ ros2 launch turtlebot3_gazebo turtlebot3_world.launch.py
```

Em um novo terminal rodamos o Cartographer SLAM:
```
$ source install/local_setup.sh
$ export TURTLEBOT3_MODEL=waffle
$ ros2 launch turtlebot3_cartographer cartographer.launch.py use_sim_time:=True
```
Dicas para criar um bom mapa:
  + Tente dirigir o mais devagar possível.
  + Evite dirigir linearmente e girar ao mesmo tempo.
  + Não dirija muito perto dos obstáculos.

Lembrando que para teleguiar 

![image](https://user-images.githubusercontent.com/112727443/235186381-78adb2b3-a094-415a-8698-87dd8290886a.png)

Para salvar o mapa abrimos um novo terminal e rodamos:
```
ros2 run nav2_map_server map_saver_cli -f my_map
```

## Navegação

Para navegação devemos abrir a simulação no gazebo:
```
$ source install/local_setup.sh
$ export TURTLEBOT3_MODEL=waffle
$ ros2 launch turtlebot3_gazebo turtlebot3_world.launch.py
```
Em outro terminal rodamos o nodo de navegação:
```
$ source install/local_setup.sh
$ export TURTLEBOT3_MODEL=waffle
ros2 launch turtlebot3_navigation2 navigation2.launch.py use_sim_time:=True map:=$HOME/map.yaml
```
![image](https://user-images.githubusercontent.com/112727443/235209913-d182c8b6-3088-466a-b739-0e8edb280e34.png)

<sub>NOTA:map:= "Diretorio aonde foi salvo seu mapa" </sub>

**No rviz:**

Para realizar a navegação autonoma, deve se clicar em ***2D POSE ESTIMATE*** aonde estimamos a posição do nosso robô

![image](https://user-images.githubusercontent.com/112727443/235210196-1358bfb8-7e39-423a-a717-9986848cf1a2.png)

Após isso podemos clicar em ***Navigation2 GO*** selecionando um local para o robô navegar.
