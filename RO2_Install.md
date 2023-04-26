# RO2_workshop
![Badge em Desenvolvimento](http://img.shields.io/static/v1?label=STATUS&message=EM%20DESENVOLVIMENTO&color=GREEN&style=for-the-badge)
![example workflow](https://github.com/github/docs/actions/workflows/main.yml/badge.svg)

# Instalação do ros2: :robot:

Instalando o Desktop full:

```
$ sudo apt install ros-foxy-desktop python3-argcomplete
```

Direcionando a source:

```
$ source /opt/ros/foxy/setup.bash
```

Utilizamos o:

```
$ nano ~/.bashrc
```

para setar em nosso terminal.


Testando a instalação atraves dos nodos de demonstração:

```
$ ros2 run demo_nodes_cpp talker
```

Em outro terminal (ctrl + alt + t) rodamos o nodo de listener:

```
$ ros2 run demo_nodes_py listener
```

Se a instalacão estiver correta teremos a comunicação dos dois nodo.

## Sistema de Pastas no ROS2

Conferir se esta rodando a ultima versão dos pacotes do ros2:

```
$ sudo apt update
$ rosdep update
```

## Workspace

Criar uma nova Workspace:

```
$ mkdir -p ~/dev_ws/src
```

Instalar os pacotes do Ros2:

```
$ sudo apt install ros-foxy-rosbag2*
```

Os pacotes Build-from-source podem ser dividido em pacotes fornecidos pelo ROS 2 e seus desenvolvedores. Ambos devem ser colocados na pasta /src da workspace.

**Deve** ser clonado na pasta src da sua workspace, neste exemplo, no diretorio dev_ws/src.

```
$ cd ~/dev_ws/src
$ git clone https://github.com/ros/ros_tutorials.git -b foxy-devel
```

Podemos ver o que temos dentro da pasta ros_tutorials usando o ls 

```
$ cd ~/dev_ws/src/ros_tutorials
$ ls
```

Antes de Buildarmos nossa Workspace vamos checar se temos todas as dependencias para o pacote, podemos já ter, mas é recomendado checar toda vez que clonamos algo, nao queremos que depois de um longo tempo de compilação de um erro por falta de alguma dependencia...  

**Devemos estar na "raiz" da nossa workspace para rodar o rosdep.**

Rodamos primeiro o rosdep init:

```
$ sudo rosdep init
```

neste caso, estando no diretorio ~/dev_ws rodamos no rosdep:

```
$  rosdep install --from-paths src --ignore-src -r -y
```

Este comando instala magicamente todos os pacotes dos quais os pacotes na sua workspacedependem, mas estão faltando em seu computador.

Sempre lembrando de dar source por garantia antes de buildar.

```
$ source /opt/ros/foxy/setup.bash
$ colcon build --symlink-install
```

Podemos dar source indo até a raiz da nossa workspace e usando:

```
$ cd ~/dev_ws/src
$ source install/local_setup.sh
```
assim garantindo que estamos buscando os arquivos na workspace certa!
