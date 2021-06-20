# Projeto de Implementação 01
## Robôs Móveis Autônomos - UFSCar

Este é o projeto de implementação 01 da disciplina Robôs Móveis Autônomos.

### Pré-requisitos
Para executar este projeto é necessário que se tenha um ambiente com o ROS instalado. A Ubuntu na qual este projeto foi testado é o 20.04 com ROS noetic. Embora você possa criar este ambiente manualmente, recomenda-se também a utilização da máquina virtual fornecida pelo time do ETH por praticidade. As instruções para utilização desta máquina virtual estão em https://ethz.ch/content/dam/ethz/special-interest/mavt/robotics-n-intelligent-systems/rsl-dam/ROS2021/CoursePreparation_v3.pdf .
É um pré-requisito também que se tenha conhecimentos básicos do ROS já que este passo a passo não será muito detalhado nas suas orientações presumindo que quem está seguindo saiba o básico dos conceitos de workspace bem como execução do catkin.

### Instalação
Descrever aqui como instalar.
- Instalar o turtlebot3 executando os comandos abaixo:

```console
source /opt/ros/noetic/setup.bash
sudo apt-get update
sudo apt-get install ros-noetic-turtlebot3-msgs
sudo apt-get install ros-noetic-turtlebot3
```

Atenção, se o comando apt-get update ou qualquer um da instalação do ros-noetic retornar um erro de chaves, o comando abaixo deve resolver o problema.

```console
curl -s https://raw.githubusercontent.com/ros/rosdistro/master/ros.asc | sudo apt-key add -
```

Em seguida, vá até a pasta src do seu workspace e digite os comandos abaixo.

```console
git clone -b noetic-devel https://github.com/ROBOTIS-GIT/turtlebot3
git clone -b noetic-devel https://github.com/ROBOTIS-GIT/turtlebot3_simulations
git clone https://github.com/fazildgr8/ros_autonomous_slam.git
git clone https://github.com/egnascimento/rma_project_01.git
catkin build
source devel/setup.bash
```
Após estas etapas o ambiente está pronto pra ser executado. As linhas abaixo escolhem o modelo de robô a ser executado e na sequência executam o launch com todos os nodes necessários para preparar o ambiente e levar o robô do ponto de origem ao ponto de destino propostos no exercício.

```console
export TURTLEBOT3_MODEL=burger
export GAZEBO_MODEL_PATH=$GAZEBO_MODEL_PATH/home/ros/Workspaces/smb_ws/src/rma_project_01/models:
roslaunch rma_project_01 rma_project_01.launch
```

Atenção: pode ser necessário editar o comando de export acima para refletir o caminho correto da sua pasta models dentro do projeto rma_project_01 que contém os modelos maze e grass_plane.

Se todos os passos forem executados com sucesso, será possível observar algo similar ao vídeo abaixo:

[![Vídeo do Projeto de Implementação 01](https://img.youtube.com/vi/bRPj9qMq97k/0.jpg)](https://www.youtube.com/watch?v=bRPj9qMq97k)

### Elaboração do mapa de custos
O mapa de custos foi elaborado utilizando o Super Mega Bot por ter sido o robô originalmente pensado para este projeto. Seguem abaixo os passos para gerar o mapa do ambiente.

### Estratégia adotada
A estratégia que escolhida priorizou a simplicidade de implementação e a reutilização dos conceitos e ferramentas previamente experimentados durante as aulas. Sendo assim, a coordenação do robô até o destino é feita pelo 2D Nav Goal e a implementação cuida somente do envio das coordenadas destino para este node.

### Resultados obtidos
O melhor resultado obtido até o momento é de um percurso do robô da origem até o destino de 261 segundos. Existe oportunidade de otimização deste tempo através da alteração dos parâmetros do algoritmo de planejamento como velocidade máxima bem como para uma estratégia de path planning que trace caminhos mais curtos mesmo que menos conservadores com relação ao desvio de obstáculos.


