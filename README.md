# Lab5_Forward_kinematics_Phantomx100
<!-- ✦✦✦ FUTURE IS AUTOMATED ✦✦✦ -->

<div align="center">

<!-- Banner superior "neón" -->
<img src="https://capsule-render.vercel.app/api?type=waving&height=200&color=0:04041A,50:14213D,100:0A4D68&text=Laboratorio%205&fontColor=E0FBFC&fontSize=60&fontAlign=50&fontAlignY=35&desc=Pincher%20Phantom%20X100%20•%20ROS%20Humble%20•%20RVIZ%20•%20Control%20y%20Conexión%20con%20Python&descSize=20&descAlign=50&descAlignY=55" width="100%" />

<br/>

# 🤖 LABORATORIO 5 – PINCHER PHANTOM X100 - ROS HUMBLE - RVIZ

<br/>

![ROS 2 Humble](https://img.shields.io/badge/ROS%202-Humble-blue?style=for-the-badge)
![Dynamixel AX-12](https://img.shields.io/badge/Dynamixel%20AX-12-green?style=for-the-badge)
![Phantom X-100](https://img.shields.io/badge/Phantom%20X-100-red?style=for-the-badge)

<br/>

<!-- Línea de texto mecanografiado (animado) -->
<p align="center">
  <img src="https://readme-typing-svg.demolab.com?font=JetBrains+Mono&weight=600&size=20&pause=1200&duration=3500&color=00E5FF&center=true&vCenter=true&width=1000&lines=Pincher+Phantom+X100+%E2%80%A2+ROS+2+Humble+%E2%80%A2+RVIZ;Control+de+Articulaciones+%E2%80%A2+Servicios+%E2%80%A2+Conexi%C3%B3n+con+Python" alt="typing">
</p>


---

### 🛰️ Descripción general

Este repositorio implementa el **Laboratorio No. 5** de *Robótica 2025-II*: control y conexión del robot **Phantom X100** utilizando **ROS 2 Humble** y **RVIZ**.  
Se incluyen tópicos de movimiento para las articulaciones, la conexión con los servomotores Dynamixel AX-12, y el control mediante Python para manipular el robot en RVIZ.

---

## 🧑‍🚀 Equipo

<!-- ===== INICIO BLOQUE ANIMACIONES EQUIPO (una animación por línea) ===== -->

<!-- Encabezado: Integrantes -->
<p align="center">
  <img src="https://readme-typing-svg.demolab.com?font=JetBrains+Mono&weight=800&size=22&duration=2000&pause=800&color=00E5FF&center=true&vCenter=true&width=1000&repeat=true&v=1&lines=Integrantes%3A" alt="Integrantes">
</p>

<!-- Nombre 1 -->
<p align="center">
  <img src="https://readme-typing-svg.demolab.com?font=JetBrains+Mono&weight=700&size=20&duration=2400&pause=600&color=7F5AF0&center=true&vCenter=true&width=1000&repeat=true&v=1&lines=Jorge+Nicol%C3%A1s+Garz%C3%B3n+Acevedo+%E2%80%94+jngarzona%40unal.du.co" alt="Jorge Nicolás Garzón Acevedo">
</p>

<!-- Nombre 2 -->
<p align="center">
  <img src="https://readme-typing-svg.demolab.com?font=JetBrains+Mono&weight=700&size=20&duration=2400&pause=600&color=7F5AF0&center=true&vCenter=true&width=1000&repeat=true&v=1&lines=Johan+Camilo+Pati%C3%B1o+Mogoll%C3%B3n+%E2%80%94+jopatinom%40unal.edu.co" alt="Johan Camilo Patiño Mogollón">
</p>

<!-- Nombre 3 -->
<p align="center">
  <img src="https://readme-typing-svg.demolab.com?font=JetBrains+Mono&weight=700&size=20&duration=2400&pause=600&color=7F5AF0&center=true&vCenter=true&width=1000&repeat=true&v=1&lines=Gabriel+Eduardo+Bojaca+Munar+%E2%80%94+gbojaca%40unal.edu.co" alt="Gabriel Eduardo Bojaca Munar">
</p>

<!-- Encabezado: Docentes -->
<p align="center">
  <img src="https://readme-typing-svg.demolab.com?font=JetBrains+Mono&weight=800&size=22&duration=2000&pause=800&color=00E5FF&center=true&vCenter=true&width=1000&repeat=true&v=1&lines=Docentes%3A" alt="Docentes">
</p>

<!-- Docente 1 -->
<p align="center">
  <img src="https://readme-typing-svg.demolab.com?font=JetBrains+Mono&weight=700&size=20&duration=2400&pause=600&color=39D353&center=true&vCenter=true&width=1000&repeat=true&v=1&lines=Manuel+Felipe+Carranza+Montenegro+%E2%80%94+mcarranza%40unal.edu.co" alt="Manuel Felipe Carranza Montenegro">
</p>

<!-- Docente 2 -->
<p align="center">
  <img src="https://readme-typing-svg.demolab.com?font=JetBrains+Mono&weight=700&size=20&duration=2400&pause=600&color=39D353&center=true&vCenter=true&width=1000&repeat=true&v=1&lines=Pedro+Fabi%C3%A1n+C%C3%A1rdenas+Herrera+%E2%80%94+pfcardenash%40unal.edu.co" alt="Pedro Fabián Cárdenas Herrera">
</p>

<!-- ===== FIN BLOQUE ANIMACIONES EQUIPO ===== -->

</div>

---


## Video de simulación y entorno físico

Video donde se evidencia la simulación en RViz y el comportamiento del robot en el entorno físico (poses y uso de la interfaz gráfica):

[![Video de simulación y entorno físico](https://img.youtube.com/vi/65TIC8xtnyM/0.jpg)](https://youtu.be/65TIC8xtnyM)

</div>

---

# Laboratorio 5 - Pincher Phantom X100 - ROS Humble - RVIZ

## Objetivos del laboratorio

1. **Crear todos los Joint Controllers** con ROS para manipular servomotores Dynamixel AX-12 del robot Phantom X Pincher.
2. **Manipular los tópicos de estado y comando** para todos los Joint Controllers del robot, entendiendo la diferencia entre:
   - Tópicos de *estado* (lectura de posición, velocidad, corriente, etc.).
   - Tópicos de *comando* (referencias de posición/velocidad para cada articulación).
3. **Manipular servicios ROS 2** asociados a los Joint Controllers (por ejemplo, habilitar/deshabilitar torque, reiniciar controladores o mover a la posición *home*).
4. **Conectar el robot Phantom X Pincher con Python usando ROS 2**, de forma que:
   - Pueda enviarse una configuración articular desde Python al robot.
   - Se reciba el estado articular para validación y visualización.
   - Se integre con herramientas de modelado (toolbox) para graficar la configuración.

## Requisitos
- Ubuntu versión 22.xx preferible 22.04 LTS con ROS Humble.
- Espacio de trabajo para `colcon build` correctamente configurado.
- Paquetes de Dynamixel Workbench: [Dynamixel Workbench GitHub](https://github.com/labsir-un/ROB_Intro_ROS2_Humble_Phantom_Pincher_X100.git)
- Paquete del robot Phantom X: [Phantom X GitHub](https://github.com/labsir-un/ROB_Intro_ROS2_Humble_Phantom_Pincher_X100_RVIZ.git)
- Python.
- Un manipulador Phantom X Pincher con su entorno de trabajo.


## Desarrollo del ejercicio en el laboratorio

### Mediciones

Las longitudes de cada eslabón del Phantom X Pincher se midieron sobre el manipulador real empleando un calibrador digital, tomando como referencia los ejes de rotación definidos en la guía del laboratorio. Para garantizar coherencia con el modelo CAD y con la posterior simulación, estas medidas se contrastaron con la información geométrica disponible en el repositorio de modelos 3D del kit:

- [`3DModels_KIT_Phantom_Pincher_X100`](https://github.com/labsir-un/3DModels_KIT_Phantom_Pincher_X100)

En particular, se revisaron las carpetas asociadas al **Phantom X Pincher** y al **kit de ensamble**, donde se almacenan las mallas y planos del robot (archivos `.stl` y documentación en PDF). Con ello se verificó que las longitudes físicas de los eslabones coincidieran con la segmentación usada en las mallas (base, hombro, brazo superior, antebrazo y gripper), lo que permitió después reutilizar esas mismas mallas en el modelo URDF/XACRO sin inconsistencias de escala ni de alineamiento.

A partir de las medidas definitivas se elaboró un diagrama esquemático análogo al de la Figura 2 de la guía, rotulando cada eslabón, su longitud efectiva y la posición relativa de las juntas.


![Posicion_Home](https://github.com/user-attachments/assets/15f08f85-9d68-445b-8a68-e5012e64596a)

![Modelado](https://github.com/user-attachments/assets/feb1e75e-651d-48e9-869d-ef925b694ff7)


### Tabla de parámetros Denavit–Hartenberg del manipulador

La siguiente tabla resume el modelo cinemático del brazo utilizado en el laboratorio, construido a partir de la posición HOME (eslabones verticales L₁, L₂, L₃ y L₄).  
Los parámetros dᵢ y aᵢ se expresan en función de las longitudes medidas de cada eslabón, mientras que los ángulos αᵢ corresponden a la rotación entre los ejes zᵢ y zᵢ₊₁.  
La columna **Offset** indica el desplazamiento angular fijo que se suma a θᵢ para que la postura HOME coincida con la configuración física del robot.

| Junta i | θᵢ  | dᵢ  | aᵢ  | αᵢ   | Offset |
|--------|-----|-----|-----|------|--------|
| 1      | θ₁  | L₁  | 0   | −90° | −90°   |
| 2      | θ₂  | 0   | L₂  | 0°   | −80°   |
| 3      | θ₃  | 0   | L₃  | 0°   | 0°     |
| 4      | θ₄  | 0   | L₄  | 0°   | 0°     |

> Nota: en el diagrama de HOME se midieron aproximadamente  
> L₁ = 4,5 cm, L₂ = 10,7 cm, L₃ = 10,7 cm y L₄ = 10,88 cm.  
> Estos valores pueden utilizarse tanto en el toolbox de robótica como en los modelos URDF/XACRO del robot.



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

### Configuración del entorno (Setup)

La preparación del entorno se realizó tomando como base tres fuentes principales:

- Sección **Setup** del kit:  
  [`KIT_Phantom_X_Pincher_ROS2`](https://github.com/labsir-un/KIT_Phantom_X_Pincher_ROS2)
- Guía 04 – creación del paquete `pincher_control` en ROS 2 Humble:  
  [`ROB_Intro_ROS2_Humble_Phantom_Pincher_X100`](https://github.com/labsir-un/ROB_Intro_ROS2_Humble_Phantom_Pincher_X100)
- Guía actualizada de **Setup** para ROS 2 Jazzy/Humble:  
  [`ROB_Intro_ROS2_Humble_Phantom_Pincher_X100_Updated/guias/Setup`](https://github.com/ElJoho/ROB_Intro_ROS2_Humble_Phantom_Pincher_X100_Updated/tree/jazzy/guias/Setup)

A partir de esas guías se siguió el siguiente flujo, adaptado al proyecto final:

1. **Creación del workspace y clonación de paquetes base**  
   Se creó el workspace `phantom_ws` y dentro de `src` se clonaron los repositorios de ejemplo recomendados en las guías (demos de simulación y/o paquetes de control), para utilizarlos como plantilla de estructura y archivos de configuración.

2. **Instalación de dependencias**  
   Se instalaron las dependencias de ROS 2 y de la librería `dynamixel_sdk` tal como se indica en las guías de control (comandos `rosdep install`, paquetes `ros-humble-dynamixel-sdk`, `python3-serial`, etc.). Esto permitió compilar el workspace con `colcon build` sin conflictos de dependencias.

3. **Configuración de hardware**  
   Se configuró el puerto serie (`/dev/ttyUSB0` o similar) y se añadió el usuario al grupo `dialout` para tener permisos sobre el adaptador USB2Dynamixel, siguiendo los pasos documentados en la Guía 04. También se verificó que los servomotores AX-12A/XL-430 tuvieran IDs únicos y compatibles con las listas definidas en los scripts de control.

4. **Scripts de lanzamiento**  
   Aprovechando la estructura propuesta en los repositorios del kit, se añadieron scripts y archivos `launch` dentro de `phantom_ws/src` para:
   - Lanzar el nodo de control y la HMI.
   - Abrir RViz con el modelo del robot y el `robot_state_publisher`.
   - Cargar la configuración de MoveIt 2 para planificación de trayectorias.

Con esta preparación, el workspace `phantom_ws` quedó listo para compilar y lanzar el sistema completo (robot real + RViz + MoveIt + HMI) desde un único entorno.

### Implementación en ROS 2 y MoveIt

El desarrollo de la parte de simulación y planificación tomó como referencia directa las guías de control y visualización:

- Control y workspace base:  
  [`ROB_Intro_ROS2_Humble_Phantom_Pincher_X100`](https://github.com/labsir-un/ROB_Intro_ROS2_Humble_Phantom_Pincher_X100)
- Control + RViz + HMI con `pincher_description` y `pincher_control`:  
  [`ROB_Intro_ROS2_Humble_Phantom_Pincher_X100_RVIZ`](https://github.com/labsir-un/ROB_Intro_ROS2_Humble_Phantom_Pincher_X100_RVIZ)
- Kit general con secciones RVIZ y MoveIt:  
  [`KIT_Phantom_X_Pincher_ROS2`](https://github.com/labsir-un/KIT_Phantom_X_Pincher_ROS2)
- Guía actualizada de MoveIt 2:  
  [`ROB_Intro_ROS2_Humble_Phantom_Pincher_X100_Updated/guias/Moveit`](https://github.com/ElJoho/ROB_Intro_ROS2_Humble_Phantom_Pincher_X100_Updated/tree/jazzy/guias/Moveit)

1. **Descripción del robot y RViz**  
   - Se construyó un paquete de descripción análogo a `pincher_description`, que importa las mallas del Phantom desde `3DModels_KIT_Phantom_Pincher_X100` y define la cinemática en un archivo `robot.xacro`.  
   - Se creó un archivo `display.launch.py` que lanza `robot_state_publisher` y RViz con una configuración predefinida, tal como se propone en la guía de RViz, cargando el modelo 3D del robot y leyendo de `/joint_states`.

2. **Configuración de MoveIt 2**  
   - Siguiendo la guía de MoveIt actualizada, se definió un grupo de planificación que incluye las articulaciones `waist`, `shoulder`, `elbow`, `wrist` y el `gripper` como efector final.  
   - Se configuraron los límites articulares, la escena de colisión y las plantillas de planificación para poder generar y ejecutar trayectorias desde la interfaz de *Motion Planning* en RViz.

3. **Nodos de control en ROS 2**  
   - Partiendo del paquete `pincher_control` descrito en la Guía 04 (control básico de servomotores con `dynamixel_sdk`), se integraron las extensiones de la Guía 05: publicación en `/joint_states`, conversión de pasos Dynamixel a radianes (`dxl_to_radians`) y corrección de signos por articulación para que la simulación y el robot real se muevan de forma coherente.  
   - Estos nodos se adaptaron y ubicaron dentro de `phantom_ws/src`, integrándolos con el resto de paquetes del proyecto final.

4. **Secuencias de movimiento y pruebas con MoveIt 2**  
   - Se programó una rutina de movimiento entre una postura de *home* y varias posturas objetivo, ejecutada de forma secuencial desde la base hasta el efector final, con pequeñas pausas entre articulaciones.  
   - Desde MoveIt 2 se planearon trayectorias hacia las poses de prueba, verificando la ausencia de colisiones y la factibilidad cinemática antes de enviar los comandos al robot real.

Gracias a esta integración, los mismos valores articulares se emplean en el controlador de los servos, en las trayectorias de MoveIt 2 y en la visualización de RViz, todo dentro del workspace `phantom_ws`.

### Conexión con Python

La conexión directa con ROS 2 y los servomotores se resolvió mediante scripts en Python, basados en las guías de control:

- Nodo `pincher_control` con `dynamixel_sdk` y `rclpy` de la Guía 04:  
  [`ROB_Intro_ROS2_Humble_Phantom_Pincher_X100`](https://github.com/labsir-un/ROB_Intro_ROS2_Humble_Phantom_Pincher_X100)
- Extensiones con publicación de `/joint_states` y GUI en Tkinter de la Guía 05:  
  [`ROB_Intro_ROS2_Humble_Phantom_Pincher_X100_RVIZ`](https://github.com/labsir-un/ROB_Intro_ROS2_Humble_Phantom_Pincher_X100_RVIZ)

Sobre esa base se implementaron dos tipos de scripts:

- **Publicadores de comando articular**  
  Scripts que reciben vectores de ángulos \([q_1, \dots, q_5]\) en grados, los convierten a unidades de los Dynamixel (0–4095 o radianes, según configuración), verifican los límites de cada junta y publican en los tópicos de control de cada articulación.

- **Lectores de estado articular**  
  Scripts suscriptores a `/joint_states` y/o a los tópicos de estado de los controladores, que leen las posiciones actuales articular por articular, las convierten a grados y devuelven la configuración \([q_1, \dots, q_5]\). Estos scripts alimentan la HMI, permiten diagnosticar el comportamiento de los servos y sirven de puente entre el robot real y el modelo cinemático usado en el toolbox.

Todos estos scripts se integraron en `phantom_ws/src` dentro del repositorio `robotica-proyecto-final`, manteniendo la misma lógica de paquetes e `entry_points` que las guías de referencia.

### Python + ROS + Toolbox

Sobre la tabla DH construida al inicio se desarrolló un módulo de Python que integra:

- El modelo cinemático directo del Phantom X Pincher.
- La lectura de configuraciones articulares desde ROS 2.
- La representación gráfica del manipulador en un entorno 3D tipo toolbox de robótica.

Este módulo adopta la nomenclatura de juntas (`waist`, `shoulder`, `elbow`, `wrist`, `gripper`) y el rango de movimiento que se documentan en las guías del kit y en el paquete `pincher_description`, de forma que:

1. Se recibe un vector \([q_1, q_2, q_3, q_4, q_5]\) (en grados o radianes) y se corrigen offsets y signos según la convención usada en los Dynamixel.
2. Se calcula la pose cartesiana del TCP (posición y orientación RPY).
3. Se genera una gráfica 3D de la configuración, comparable con la visualización en RViz/MoveIt 2.
4. Se actualiza la figura en función de las lecturas de `/joint_states`, permitiendo comparar la pose digital (toolbox) con la pose real del manipulador.

### Poses de prueba

Para validar el modelo, la configuración de MoveIt 2 y la implementación de los nodos de control, se ensayaron de forma sistemática las siguientes configuraciones articulares \((q_1, q_2, q_3, q_4, q_5)\) en grados:

1. \(0, 0, 0, 0, 0\)  
2. \(25, 25, 20, -20, 0\)  
3. \(-35, 35, -30, 30, 0\)  
4. \(85, -20, 55, 25, 0\)  
5. \(80, -35, 55, -45, 0\)

Cada una de estas poses se probó:

- En el robot físico, verificando que ninguna articulación excediera sus límites y que no hubiera interferencia con la mesa ni con otros elementos.
- En MoveIt 2, comprobando la existencia de soluciones cinemáticas y trayectorias libres de colisión.
- En la representación del toolbox, comparando la pose cartesiana calculada con la que observa el operador en RViz.

### Interfaz de Usuario (HMI)

La HMI desarrollada en el proyecto está fuertemente inspirada en la interfaz Tkinter descrita en la Guía 05 del repositorio de RViz, donde se propone una ventana con pestañas para:

- Sliders de control en tiempo real.
- Entrada numérica de comandos.
- Lanzamiento y cierre de RViz desde botones dedicados.

Tomando como punto de partida esa estructura, la HMI del proyecto final (ubicada en `phantom_ws/src` de `robotica-proyecto-final`) se extendió para incluir:

1. **Panel de identificación**  
   Muestra nombres, logos y datos de contacto de los integrantes del grupo, siguiendo la estética institucional del curso.

2. **Visualización de la última posición enviada**  
   Incluye una imagen/captura asociada a la última configuración enviada al robot (ya sea foto del manipulador o captura de RViz), utilizada también para documentar resultados.

3. **Selección de poses predefinidas**  
   Botones que cargan directamente las cinco poses de prueba y envían los vectores articulares correspondientes al nodo de control, reutilizando la misma lógica que se describe en los scripts de `pincher_control`.

4. **Lectura de ángulos articulares en tiempo real**  
   Un panel numérico que muestra la lectura actual de cada junta a partir de `/joint_states`, sincronizada con el movimiento del robot.

5. **Visualización de la posición actual**  
   Un área gráfica que refleja la pose actual del manipulador, facilitando la comparación entre el comando enviado y la configuración realmente alcanzada.

### Funcionalidades de la interfaz gráfica

La HMI se organizó en varias pestañas, ampliando las ideas de la GUI original de `pincher_control`:

- **Pestaña de control en espacio articular**  
  Contiene sliders para cada articulación, con límites configurados según las especificaciones del Phantom. Al mover un slider:
  1. Se actualiza el valor numérico mostrado.
  2. Se envía el comando articular vía ROS 2 al nodo de control.
  3. Se actualiza en paralelo la visualización en RViz/MoveIt y en la propia HMI.

- **Pestaña de ingreso numérico articular**  
  Permite escribir directamente los valores de \(q_1\) a \(q_5\) en grados. Antes de publicar:
  1. Se validan los rangos de seguridad.
  2. Se corrigen o se rechazan valores fuera de rango.
  3. Se sincronizan tanto la vista de RViz como los indicadores numéricos.

- **Pestaña de control en el espacio de la tarea**  
  Brinda controles para desplazar el TCP en \(X, Y, Z\) y ajustar la orientación en RPY. Internamente:
  1. Se resuelve la cinemática inversa con el modelo DH.
  2. Se comprueba la alcanzabilidad y el cumplimiento de límites.
  3. Se envía la nueva configuración articular al robot real y a la simulación.

- **Pestaña de visualización en RViz/MoveIt**  
  Reutiliza la lógica propuesta en la Guía 05 para lanzar y cerrar RViz desde la propia HMI, ejecutando comandos tipo `ros2 launch pincher_description display.launch.py`. El modelo del Phantom se actualiza con los valores de `/joint_states`, logrando una visualización sincronizada del movimiento real.

- **Pestaña de visualización numérica de la pose cartesiana**  
  Muestra en tiempo real la posición \(X, Y, Z\) y la orientación (Roll–Pitch–Yaw) del TCP calculadas a partir del modelo cinemático y de la configuración articular actual. Esta información es clave para comparar resultados entre:
  - El modelo analítico (toolbox).
  - La simulación en RViz/MoveIt.
  - El comportamiento del robot físico.

En conjunto, el desarrollo del laboratorio se apoya en los siguientes repositorios de referencia, de los cuales se adaptaron estructuras de paquetes, modelos 3D, nodos de control, guías de configuración y ejemplos de GUI:

- [`KIT_Phantom_X_Pincher_ROS2`](https://github.com/labsir-un/KIT_Phantom_X_Pincher_ROS2)  
- [`ROB_Intro_ROS2_Humble_Phantom_Pincher_X100`](https://github.com/labsir-un/ROB_Intro_ROS2_Humble_Phantom_Pincher_X100)  
- [`ROB_Intro_ROS2_Humble_Phantom_Pincher_X100_RVIZ`](https://github.com/labsir-un/ROB_Intro_ROS2_Humble_Phantom_Pincher_X100_RVIZ)  
- [`3DModels_KIT_Phantom_Pincher_X100`](https://github.com/labsir-un/3DModels_KIT_Phantom_Pincher_X100)  
- [`ROB_Intro_ROS2_Humble_Phantom_Pincher_X100_Updated/guias/Setup`](https://github.com/ElJoho/ROB_Intro_ROS2_Humble_Phantom_Pincher_X100_Updated/tree/jazzy/guias/Setup)  
- [`ROB_Intro_ROS2_Humble_Phantom_Pincher_X100_Updated/guias/Moveit`](https://github.com/ElJoho/ROB_Intro_ROS2_Humble_Phantom_Pincher_X100_Updated/tree/jazzy/guias/Moveit)  
- [`sergiosinlimites/robotica-proyecto-final/phantom_ws/src`](https://github.com/sergiosinlimites/robotica-proyecto-final/tree/main/phantom_ws/src)


---
## Plano de planta de la ubicación de cada uno de los elementos
---
## Diagrama de flujo de acciones del robot utilizando la herramienta Mermaid





