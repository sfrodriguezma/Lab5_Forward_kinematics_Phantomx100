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

Con las dimensiones finales se construyó la tabla de parámetros Denavit–Hartenberg (DH) del Phantom X Pincher, siguiendo la convención de marcos utilizada en los ejemplos de ROS 2 para este robot. La asignación de marcos y los nombres de las juntas (`waist`, `shoulder`, `elbow`, `wrist`, `gripper`) se alinearon con la estructura propuesta en los paquetes de descripción y control del ecosistema Phantom:

- Guía de control en ROS 2 Humble para el Phantom X Pincher:  
  [`ROB_Intro_ROS2_Humble_Phantom_Pincher_X100`](https://github.com/labsir-un/ROB_Intro_ROS2_Humble_Phantom_Pincher_X100)
- Guía de descripción y visualización en RViz:  
  [`ROB_Intro_ROS2_Humble_Phantom_Pincher_X100_RVIZ`](https://github.com/labsir-un/ROB_Intro_ROS2_Humble_Phantom_Pincher_X100_RVIZ)

En la guía de RViz se detalla la creación de un paquete de descripción `pincher_description` con un archivo `robot.xacro` y un conjunto de mallas segmentadas (`px100_1_base.stl`, `px100_2_shoulder.stl`, `px100_3_upper_arm.stl`, etc.) que se organizan dentro de una carpeta `meshes/`. A partir de esa referencia se ajustaron los parámetros \(a_i\), \(\alpha_i\), \(d_i\) y \(\theta_i\) para que:

- La cinemática usada en la tabla DH fuese compatible con la cadena de transformaciones codificada en el `robot.xacro`.
- La orientación de cada marco DH fuera consistente con la que utiliza `robot_state_publisher` para publicar `/robot_description`.

El resultado fue una tabla DH que sirve tanto para el toolbox de robótica en Python como para la descripción URDF/XACRO del robot, garantizando que la pose cartesiana obtenida analíticamente coincida con la visualización en RViz.

---

### Organización del repositorio y workspace `phantom_ws`

Todo el desarrollo se consolidó en el repositorio de proyecto final:

- [`sergiosinlimites/robotica-proyecto-final`](https://github.com/sergiosinlimites/robotica-proyecto-final)

Dentro de este repositorio se creó un workspace ROS 2 específico para el Phantom X Pincher:

- Workspace: `phantom_ws`
- Código fuente: `phantom_ws/src`

La organización de `phantom_ws/src` sigue la filosofía propuesta en los repositorios del kit oficial:

- [`KIT_Phantom_X_Pincher_ROS2`](https://github.com/labsir-un/KIT_Phantom_X_Pincher_ROS2)
- [`ROB_Intro_ROS2_Humble_Phantom_Pincher_X100`](https://github.com/labsir-un/ROB_Intro_ROS2_Humble_Phantom_Pincher_X100)
- [`ROB_Intro_ROS2_Humble_Phantom_Pincher_X100_RVIZ`](https://github.com/labsir-un/ROB_Intro_ROS2_Humble_Phantom_Pincher_X100_RVIZ)

Siguiendo esas referencias, el workspace se estructuró en paquetes que agrupan:

- **Descripción del robot**: modelo URDF/XACRO y mallas importadas desde `3DModels_KIT_Phantom_Pincher_X100`.
- **Control articular y conexión Dynamixel**: nodos en Python basados en el paquete `pincher_control` descrito en las guías 04 (control del robot) y 05 (control + RViz).
- **Integración con RViz y MoveIt 2**: paquetes y archivos de lanzamiento para cargar el modelo, la escena y la configuración de planificación.
- **Interfaz gráfica (HMI)**: scripts en Python que implementan las pestañas de control articular, cartesiano, visualización en RViz y lectura de estados.

De esta forma, `robotica-proyecto-final` actúa como contenedor de todo el entorno funcional del laboratorio (código, configuración y herramientas) sobre un único workspace `phantom_ws`, compatible con la estructura propuesta en los repositorios de referencia del curso.

---

### Configuración del entorno (Setup)

La preparación del entorno se realizó tomando como base tres fuentes principales:

- Sección **Setup** del kit:  
  [`KIT_Phantom_X_Pincher_ROS2`](https://github.com/labsir-un/KIT_Phantom_X_Pincher_ROS2)
- Guía 04 – creación del paquete `pincher_control` en ROS 2 Humble:  
  [`ROB_Intro_ROS2_Humble_Phantom_Pincher_X100`](https://github.com/labsir-un/ROB_Intro_ROS2_Humble_Phantom_Pincher_X100)
- Guía actualizada de **Setup** para ROS 2 Jazzy/Humble:  
  [`ROB_Intro_ROS2_Humble_Phantom_Pincher_X100_Updated/guias/Setup`](https://github.com/ElJoho/ROB_Intro_ROS2_Humble_Phantom_Pincher_X100_Updated/tree/jazzy/guias/Setup)

El flujo seguido:

1. **Creación del workspace y clonación de paquetes base**  
2. **Instalación de dependencias** (`rosdep`, `dynamixel_sdk`, `python3-serial`, etc.)  
3. **Configuración de hardware** (puerto serie, permisos `dialout`, IDs Dynamixel).  
4. **Scripts de lanzamiento** para control, RViz y MoveIt.

Así, el workspace quedó listo para lanzar robot real + RViz + MoveIt + HMI desde un solo entorno.

---

### Implementación en ROS 2 y MoveIt

1. **Descripción del robot y RViz**  
2. **Configuración de MoveIt 2** (grupo de planificación, límites, colisiones).  
3. **Nodos de control con `dynamixel_sdk`** (publicación de `/joint_states`, corrección de signos).  
4. **Secuencias de movimiento y pruebas con MoveIt**.

Todo sincronizado entre simulación, modelo cinemático y robot real.

---

### Conexión con Python

Se implementaron scripts para:

- **Publicar comandos articulares**
- **Leer estado en tiempo real**
- **Convertir unidades Dynamixel ↔ radianes**

Integrados en ROS 2 y en el toolbox.

---

### Python + ROS + Toolbox

El módulo Python combina:

- Modelo cinemático directo DH  
- Lectura desde ROS 2  
- Visualización 3D tipo toolbox  

Permite comparar:

- Pose analítica  
- Pose en RViz/MoveIt  
- Pose del robot real  

---

### Poses de prueba

Las configuraciones evaluadas fueron:

1. \(0, 0, 0, 0, 0\)  
2. \(25, 25, 20, -20, 0\)  
3. \(-35, 35, -30, 30, 0\)  
4. \(85, -20, 55, 25, 0\)  
5. \(80, -35, 55, -45, 0\)

Probadas en robot físico, MoveIt y toolbox.

---

### Interfaz de Usuario (HMI)

Basada en la GUI de la Guía 05, extendida con:

1. **Panel de identificación**  
2. **Visualización de la última posición**  
3. **Botones con poses predefinidas**  
4. **Lectura articulada en tiempo real**  
5. **Visualización gráfica del robot**

---

### Funcionalidades de la UI

Organizada en pestañas:

- **Control articular con sliders**  
- **Ingreso numérico articular**  
- **Control cartesiano + IK**  
- **Visualización en RViz/MoveIt**  
- **Pose cartesiana (XYZ + RPY)**  

Con sincronización total robot ↔ ROS ↔ RViz ↔ toolbox.

---












 