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
Ubuntu 16.04 (Xenial), existen dos `distribuciones de ROS <https://www.ros.org/reps/rep-0003.html#noetic-ninjemys-may-2020-may-2025>`_ soportadas por 
Ubuntu 16.04: Kinetic Kame y Lunar Loggerhead. 
Por tanto se comenzó ingenuamente a 
trabajar con Melodic. El problema que más adelante surgió es que 
Melodic soporta oficialmente Python 2.7, versiones mayores a 2.7 presentan
problemas. Para trabajar con Tensorflow se requiere Python >= 3.5 
(aunque es posible usarlo con Python<3.5 , se tendrían que usar versiones
antiguas de Tensorflow, pero es más complicado ajustar algoritmos y 
redes neuronales para usarse con paqueterías antiguas).


**Solución:** En Mayo 2020 salió la distribución de ROS Noetic Ninjemys, que 
soporta Python 3.8, y es soportada por Ubuntu 20.04 Focal Fossa.


**Nuevo Problema:** Al ser relativamente nueva esta distribución (ROS Noetic)
algunos paquetes para simulación, principalemte 
husky_gazebo aún no tienen soporte para la misma.


**Solución:** El 8 de Septiembre del 2020, el equipo de husky  
comentó en `su cuenta de Github <https://github.com/husky/husky/issues/136>`_ que 
planeaban comenzar a trabajar en un lazamiento para Noetic en 2020, y que se
tenían la intención de tener soporte "pronto".


Se pueden modificar los códigos de los paquetes de simulación del husky
y tratar que sean compatibles para Noetic, pero no es recomendable pues
ya hay un equipo especializado en eso, y hay otras areas (para este proyecto)
de aprendizaje.

.. topic:: Conclusión

    Se recomienda usar Ubuntu 20.04 
    (Focal Fossa) con ROS Noetic. Aunque las instrucciones 
    subsecuentes
    esten para otras versiones se intentarán cubrir algunas posibles
    diferencias.




Get Started
=============
El proyecto consta de dos etapas principales y hay un repositorio para cada etapa:

* Entrenamiento: `CustumObjectDetection <https://github.com/Daegas/CustumObjectDetection>`_ Usando Anaconda,Python, Tensorflow, Keras.
* Implementación: `multi_camera_husky <https://github.com/Daegas/multi_camera_husky>`_ Usando ROS, Gazebo y Python. 

Se tratará de explicar a grandes rasgos lo necesario para entender 
y reproducir cada etapa. 
Además se agregaran algunos links
con informaicón adicional denotados por 👁.
Prepárense para leer bastante.

.. note:: La etapa de implementación aún no está completa por los motivos expresados en la sección anterior. 


.. `installation`_
.. ⬅️   ➡️
