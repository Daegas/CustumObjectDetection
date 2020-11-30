============
Introducción
============

El propósito del proyecto es crear una red neuronal para entrenar un modelo en tensorflow 
capaz de reconocer el robot Clearpath Husky,para posteriormente
implementar este modelo en una simulación de Gazebo y más adelante en
el robot físico.

*Si no entiendes muy bien lo que a continuación viene, puedes simplemente
leer la conclusión*

En primera instancia el proyecto comenzó a ser implementado en 
Ubuntu 16.04 (Xenial). Existen dos `distribuciones de ROS <https://www.ros.org/reps/rep-0003.html#noetic-ninjemys-may-2020-may-2025>`_ soportadas por 
Ubuntu 16.04: Kinetic Kame y Lunar Loggerhead. 
Se comenzó, ingenuamente a 
trabajar con Kinetic. El problema que más adelante surgió es que 
Kinetic soporta oficialmente Python 2.7, versiones mayores a 2.7 presentan
problemas. Para trabajar con Tensorflow se requiere Python >= 3.5 
(aunque es posible usarlo con Python<3.5 , se tendrían que usar versiones
antiguas de Tensorflow, pero es más complicado ajustar algoritmos y 
redes neuronales para usarse con paqueterías antiguas, aunque es una opción).

Después, se decidió cambiar el sistema operativo a Ubuntu 18.04 (Bionic),
pues la distribución subsecuente de Kinetic y Lunar, es decir Melodic, tiene 
soporte, auque aún de prueba, para python>=3.5.




**Dato:** En Mayo 2020 salió la distribución de ROS Noetic Ninjemys, que 
soporta oficialmente Python 3.8, y es dirigida para Ubuntu 20.04 Focal Fossa.


**Nuevo Problema:** Al ser relativamente nueva esta distribución (ROS Noetic)
algunos paquetes para simulación, principalemte 
husky_gazebo aún no tienen soporte para la misma.


**Solución:** El 8 de Septiembre del 2020, el equipo de husky  
comentó en `su cuenta de Github <https://github.com/husky/husky/issues/136>`_ que 
planeaban comenzar a trabajar en un lazamiento para Noetic a finales de 2020, y que se
tenía la intención de tener soporte "pronto".


Se pueden modificar los códigos de los paquetes de simulación del husky
y tratar que sean compatibles para Noetic, pero no es recomendable pues
ya hay un equipo especializado en eso, y hay otras áreas (para este proyecto)
de aprendizaje.




Get Started
=============
El proyecto consta de dos etapas principales y hay un repositorio para cada etapa:

* **Entrenamiento:** `CustumObjectDetection <https://github.com/Daegas/CustumObjectDetection>`_ Usando Anaconda,Python, Tensorflow, Keras.
* **Implementación:** `multi_camera_husky <https://github.com/Daegas/multi_camera_husky>`_ Usando ROS, Gazebo y Python. 

Cada etapa tiene un contexto, instalación y la aplicación final.
Se tratará de explicar a grandes rasgos lo necesario para entender 
y reproducir cada etapa. 
Además se agregaran algunos links, muchas veces en inglés,
con información adicional. Los denotados por 👁 son generalmente para conocimiento de algún tema.



.. hint:: 

    Se puede usar Ubuntu 18.04, con ROS Melodic. En cuanto salgan los paquetes de husky_gazebo
    compatibles con ROS Noetic, sería ideal trasladar el proyecto a Ubuntu 20.04 (Focal Fossa)
    para que se pueda comunicar el entrenamiento con la implementación sin problemas. 
    Ahorita se tiene documentado:

    #. Pasos para entrenar y guardar el modelo.
    #. Implementación de un modelo de Keras en un nodo que se suscribe al tópico de la cámara local del dispositivo y publica dos tópicos uno con el nombre del objeto detectado y otro con la probabilidad de que sea el objeto.


    TO DO:


    #. Entrenar el modelo con GPU o en línea, pues solo se entrenó con CPU.
    #. Hacer diferentes pruebas con diferentes modelos de model_zoo y el elegir el de mejor resultado.
    #. Guardar el modelo en formato de Keras (h5), ahorita solo de guarda en (.pb).
    #. Usar el modelo (h5) en el código que ya se tiene.
    #. Cambiar el tópico de camera/image_raw al tópico de la camara del husky o huskys.


