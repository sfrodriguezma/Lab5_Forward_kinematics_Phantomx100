 # Laboratorio No. 5 – Robótica De desarrollo– Implementacion de la cinematica directa del robot Phantom x100 con Ros2 Humble

## Integrantes

* Sergio Andrés Bolaños Penagos
* Sergio Felipe Rodriguez Mayorga

## 📝 Introducción

Este repositorio contiene los resultados y el código desarrollado para el **Laboratorio No. 05** de Robótica con enfoque en la **Cinemática Directa** del manipulador **Phantom X Pincher**. El robot utiliza servomotores **Dynamixel AX-12** y se controla y manipula utilizando **ROS Humble** en un entorno de **Ubuntu 22.04 LTS**.

El objetivo principal de esta práctica es establecer la cinemática del robot, obtener sus **parámetros DH** y desarrollar las herramientas de software necesarias para controlarlo y visualizar su estado. Esto incluye la creación y manipulación de Joint Controllers con ROS, la implementación de scripts en Python para el control de articulaciones, y el desarrollo de una Interfaz Hombre-Máquina (**HMI**) avanzada para el control en espacio articular con visualización en RViz.

## 🎯 Objetivos

* Crear todos los Joint Controllers con ROS para manipular servomotores Dynamixel AX-12 del robot Phantom X Pincher.
* Manipular los **tópicos de estado y comando** para todos los Joint Controllers del robot.
* Manipular los **servicios** para todos los Joint Controllers del robot.
* Conectar el robot Phantom X Pincher con Python usando ROS 2.
* **Desarrollar Scripts en ROS 2 y Python**:
    * Crear un script para mover las articulaciones (_waist, shoulder, elbow, wrist_) secuencialmente entre una posición *home* y una objetivo, utilizando tópicos y servicios Dynamixel en ROS.
    * Crear scripts en Python que permitan publicar y suscribirse a cada tópico del controlador de articulación, validando los límites articulares.
    * Crear código Python para enviar la posición , graficar la configuración del robot usando las herramientas de rviz, y verificar la coincidencia con el robot real.
* **Implementar Interfaz de Usuario (HMI)**:
    * Mostrar información del grupo, la posición actual, y los valores articulares reales.
    * Opción para seleccionar y enviar **5 poses predefinidas** al manipulador.
    
* Control en espacio articular .
         
         
* Visualización en RViz** que imite en tiempo real los movimientos del manipulador real.
* Visualización numérica** en tiempo real de la posición cartesiana (X, Y, Z) y orientación (RPY) del TCP.

## 💻 Requisitos

| Software/Hardware | Requisito | Fuente |
| :--- | :--- | :--- |
| **Sistema Operativo** | Ubuntu versión 22.xx (preferible 22.04 LTS) | |
| **Framework de Robótica** | ROS Humble | |
| **Entorno de Trabajo** | Espacio de trabajo para `colcon build` correctamente configurado | |
| **Lenguaje de Programación** | Python | |
| **Paquete Dynamixel** | `ROB_Intro_ROS2_Humble_Phantom_Pincher_X100.git` | |
| **Paquete Robot/RVIZ** | `ROB_Intro_ROS2_Humble_Phantom_Pincher_X100_RVIZ.git` | |
| **Hardware** | Un (1) manipulador Phantom X Pincher con su entorno de trabajo | |
### Mediciones
## Medición y Modelado de los Eslabones

Las longitudes de los eslabones del Phantom X Pincher fueron obtenidas directamente del manipulador real empleando un calibrador digital, tomando como referencia los ejes de rotación definidos en la guía del laboratorio. Para asegurar coherencia con el modelo CAD y con las simulaciones posteriores, estas mediciones se contrastaron con la información geométrica disponible en el repositorio oficial de modelos 3D del kit:

- [`3DModels_KIT_Phantom_Pincher_X100`](https://github.com/labsir-un/3DModels_KIT_Phantom_Pincher_X100)

Se revisaron particularmente las carpetas del **Phantom X Pincher** y del **kit de ensamble**, donde se encuentran las mallas y planos técnicos del robot (archivos `.stl` y documentación en PDF). Este proceso permitió validar que las longitudes medidas coincidían con la segmentación presente en las mallas del robot (base, hombro, brazo superior, antebrazo y gripper). Gracias a ello, las mismas mallas pudieron reutilizarse en el modelo URDF/XACRO sin inconsistencias de escala ni desalineamiento.

Con las dimensiones finales se construyó un diagrama esquemático similar al de la Figura 2 de la guía, indicando cada eslabón, su longitud efectiva y la ubicación relativa de las juntas.

### 📸 Imágenes de Referencia

![Posicion_Home](https://github.com/user-attachments/assets/15f08f85-9d68-445b-8a68-e5012e64596a)

![Modelado](https://github.com/user-attachments/assets/feb1e75e-651d-48e9-869d-ef925b694ff7)

### Tabla de parámetros Denavit–Hartenberg del manipulador

La siguiente tabla presenta el modelo cinemático del brazo empleado en el laboratorio, tomando como referencia la posición HOME, donde los eslabones L₁, L₂, L₃ y L₄ se encuentran en orientación vertical.
Los parámetros dᵢ y aᵢ dependen directamente de las longitudes medidas de cada eslabón, mientras que los ángulos αᵢ representan la rotación relativa entre los ejes zᵢ y zᵢ₊₁.
La columna Offset corresponde al ángulo constante que debe añadirse a θᵢ para que la postura HOME coincida correctamente con la configuración física real del manipulador.

| Junta i | θᵢ  | dᵢ  | aᵢ  | αᵢ   | Offset |
|--------|-----|-----|-----|------|--------|
| 1      | θ₁  | L₁  | 0   | −90° | −90°   |
| 2      | θ₂  | 0   | L₂  | 0°   | −80°   |
| 3      | θ₃  | 0   | L₃  | 0°   | 0°     |
| 4      | θ₄  | 0   | L₄  | 0°   | 0°     |

 L₁ = 4,5 cm, L₂ = 10,7 cm, L₃ = 10,7 cm y L₄ = 10,88 cm. Estos valores se utilizan  tanto en el toolbox de robótica como en los modelos URDF/XACRO del robot.

### Análisis

Con las medidas finales se construyó la tabla de parámetros Denavit–Hartenberg (DH) del Phantom X Pincher, empleando la misma asignación de marcos mostrada en los ejemplos oficiales de ROS 2 para este robot. Se respetaron los nombres de las articulaciones (`waist`, `shoulder`, `elbow`, `wrist`, `gripper`) para que el modelo fuese compatible con los paquetes de descripción y control utilizados en el ecosistema Phantom:

- Guía de control en ROS 2 Humble:  
  [`ROB_Intro_ROS2_Humble_Phantom_Pincher_X100`](https://github.com/labsir-un/ROB_Intro_ROS2_Humble_Phantom_Pincher_X100)
- Guía de visualización en RViz:  
  [`ROB_Intro_ROS2_Humble_Phantom_Pincher_X100_RVIZ`](https://github.com/labsir-un/ROB_Intro_ROS2_Humble_Phantom_Pincher_X100_RVIZ)

En la guía de RViz se explica cómo crear el paquete `pincher_description`, que incluye el archivo `robot.xacro` y el conjunto de mallas segmentadas (`px100_1_base.stl`, `px100_2_shoulder.stl`, etc.). A partir de ese estándar se ajustaron los parámetros \(a_i\), \(\alpha_i\), \(d_i\) y \(\theta_i\) de manera que:

- La tabla DH fuera coherente con la cadena cinemática definida en el `robot.xacro`.
- Las orientaciones de los marcos DH coincidieran con las transformaciones publicadas por `robot_state_publisher`.

De esta forma, la tabla DH resultante funciona tanto para el toolbox de robótica en Python como para la descripción URDF/XACRO, asegurando que la pose cartesiana calculada coincida con lo visualizado en RViz.

---

### Organización del repositorio y workspace `phantom_ws`

Todo el desarrollo se integró dentro del repositorio del proyecto final:

- [`sergiosinlimites/robotica-proyecto-final`](https://github.com/sergiosinlimites/robotica-proyecto-final)

En este repositorio se creó un workspace específico para el Phantom X Pincher:

- Workspace: `phantom_ws`
- Carpeta de código: `phantom_ws/src`

La distribución interna del workspace se inspira en la estructura recomendada por los repositorios del kit oficial:

- [`KIT_Phantom_X_Pincher_ROS2`](https://github.com/labsir-un/KIT_Phantom_X_Pincher_ROS2)
- [`ROB_Intro_ROS2_Humble_Phantom_Pincher_X100`](https://github.com/labsir-un/ROB_Intro_ROS2_Humble_Phantom_Pincher_X100)
- [`ROB_Intro_ROS2_Humble_Phantom_Pincher_X100_RVIZ`](https://github.com/labsir-un/ROB_Intro_ROS2_Humble_Phantom_Pincher_X100_RVIZ)

Siguiendo este modelo, el workspace se organizó en paquetes que incluyen:

- **Descripción del robot**: archivos URDF/XACRO y mallas importadas desde `3DModels_KIT_Phantom_Pincher_X100`.
- **Control articular y comunicación Dynamixel**: nodos basados en `pincher_control` según las guías 04 y 05.
- **Integración con RViz y MoveIt 2**: configuración de planificación y archivos de lanzamiento.
- **Interfaz gráfica (HMI)**: scripts en Python para control, visualización y monitoreo.

De este modo, el repositorio `robotica-proyecto-final` centraliza todo el entorno de trabajo (código, configuración y herramientas) dentro de un único workspace `phantom_ws`, completamente alineado con los repositorios utilizados en el curso.

---

### Configuración del entorno (Setup)

La preparación del entorno se realizó tomando como referencia:

- Sección **Setup** del kit oficial:  
  [`KIT_Phantom_X_Pincher_ROS2`](https://github.com/labsir-un/KIT_Phantom_X_Pincher_ROS2)
- Guía 04 del curso (creación del paquete `pincher_control`):  
  [`ROB_Intro_ROS2_Humble_Phantom_Pincher_X100`](https://github.com/labsir-un/ROB_Intro_ROS2_Humble_Phantom_Pincher_X100)
- Versión actualizada del Setup para ROS 2 Jazzy/Humble:  
  [`ROB_Intro_ROS2_Humble_Phantom_Pincher_X100_Updated/guias/Setup`](https://github.com/ElJoho/ROB_Intro_ROS2_Humble_Phantom_Pincher_X100_Updated/tree/jazzy/guias/Setup)

El proceso consistió en:

1. **Crear el workspace y clonar los paquetes necesarios**  
2. **Instalar dependencias** como `rosdep`, `dynamixel_sdk` y `python3-serial`  
3. **Configurar el hardware** (puerto serial, permisos `dialout`, IDs de los Dynamixel)  
4. **Crear los archivos de lanzamiento** para control, RViz y MoveIt  

Esto dejó el entorno listo para ejecutar robot real, RViz, MoveIt y HMI desde un único workspace.

---

### Implementación en ROS 2 y MoveIt

El sistema se integró mediante:

1. **Modelo URDF/XACRO y visualización en RViz**  
2. **Configuración completa de MoveIt 2** (colisiones, planificación y límites articulares)  
3. **Nodos de control basados en `dynamixel_sdk`**  
4. **Pruebas de movimiento usando MoveIt y comandos propios**

Todo sincronizado entre simulación, control y robot físico.

---

### Conexión con Python

Se desarrollaron scripts que permiten:

- Enviar comandos articulares  
- Leer estados en tiempo real  
- Convertir entre unidades Dynamixel y radianes  

Integrados con ROS 2 y con el toolbox de robótica.

---

### Python + ROS + Toolbox

El módulo en Python combina:

- Cinemática directa mediante DH  
- Lectura de ROS 2  
- Visualización tipo toolbox  

Lo que permite comparar:

- La pose calculada  
- La pose mostrada en RViz/MoveIt  
- La pose real del robot  

---

### Poses de prueba

Se evaluaron las siguientes configuraciones articulares:

1. \(0, 0, 0, 0, 0\)  
2. \(25, 25, 20, -20, 0\)  
3. \(-35, 35, -30, 30, 0\)  
4. \(85, -20, 55, 25, 0\)  
5. \(80, -35, 55, -45, 0\)

Probadas en el robot real y en la simulación.

---

### Interfaz de Usuario (HMI)

Basada en la interfaz de la Guía 05, ampliada con:

1. **Panel de identificación del robot**  
2. **Registro de la última posición alcanzada**  
3. **Botones de poses predefinidas**  
4. **Lectura continua del estado articular**  
5. **Visualización gráfica del robot**

---

### Funcionalidades de la UI

La interfaz se divide en pestañas que permiten:

- Control articulado mediante sliders  
- Ingreso numérico de ángulos  
- Control cartesiano con IK  
- Visualización en RViz/MoveIt  
- Lectura de pose cartesiana (XYZ + RPY)  

Todo sincronizado entre robot, simulación y toolbox.

---












 