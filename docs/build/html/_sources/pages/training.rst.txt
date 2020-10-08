=================
Entrenamiento
=================

Repositorio: `CustumObjectDetection <https://github.com/Daegas/CustumObjectDetection>`_ 


Contexto
========
El fin de esta sección es compilar información básica para entender el proceso
de entrenamiento del modelo.

Redes Neuronales Convolucionales (CNN)
----------------------------------------
Las CNN fueron introducidas por primera vez por Yann LeCun 1998 en 
`Gradient-Based Learning Applied to Document Recognition <https://pdfs.semanticscholar.org/62d7/9ced441a6c78dfd161fb472c5769791192f6.pdf>`_
y resultaron ser muy efectivas en reconocimiento de imágenes y clasificación.

👁 `¿Pero qué "es" una Red neuronal? <https://www.youtube.com/watch?v=aircAruvnKk>`_

Cómo se ve en el video una red neuronal está compuesta por capas, cada capa contiene un vector de
características que conservan una relación espacial entre pixeles.
Dada una imagen en forma de matriz:


*  👁 `Explicación Visual Kernels <https://setosa.io/ev/image-kernels/>`_ 



Se aplican filtros para resaltar bordes, circunferencias, esquinas, etc. Esta técnica para detectar las partes más importantes de una imagen se llama "convolución"  

* 👁 `Descenso de gradiente, es como las redes neuronales aprenden <https://www.youtube.com/watch?v=IHZwWFHWa-w&t=660s>`_


Con el descenso de gradiente se buscar calcular cuales valores de pesos y bias minimizan el costo, la distancia del resultado obtenido en la última capa con el resultado esperado.

* 👁 `¿Qué es la retropropagación y qué hace en realidad? <https://www.youtube.com/watch?v=Ilg3gGewQ5U>`_


Cada neurona en la penúltima capa necesita unos ajustes de parámetros (bias, pesos) para que en la última capa (salida) las neuronas más activas correspondan a las que se esperan estén más activas. Se agregan todos los ajustes de todas las neuronas de esa penúltima capa, luego se hace lo mismo con la antepenúltima y así hasta llegar a la segunda capa (la primera es la entrada). A eso se le llama "retropropagación".

**Otros datos:**


* 👁 `Funciones de Activación <https://www.i2tutorials.com/activation-functions-in-deep-learning/>`_


Cada neurona toma la una entrada, la multiplica por el peso, le agrega el bias y el resultado lo pasa por una función de activación, que son funciones que determinan si una neurona debe o no ser activada. Ayudan a normalizar en un rango [0 , 1] o [-1 , 1] Existen muchos tipos de funciones de activación (Sigmoid, ReLU, TanH, LeakyReLU, Softmax, etc) 

* Capas


El propósito de cada capa varia, a veces pueder ser reducir dimensionalidad (pooling), detectar patrones (convolución) entre otras funciones.

* 👁 `Arquitecturas <https://medium.com/analytics-vidhya/cnns-architectures-lenet-alexnet-vgg-googlenet-resnet-and-more-666091488df5>`_


Existen muchas arquitecturas, es decir cuantas capas, de que tipo y en que acomodo se usan en una red. Hay arquitecturas de redes neuronales que no tienen convolución, generalmente las usadas en reconocimiento y clasificación de imágenes si tienen. Algunas arquitecturas muy famosas de CNN especiales para detectar patrones visuales son VGG, Inception, RESNET.

* 👁 `Aquí <https://www.cs.cmu.edu/~aharley/vis/conv/flat.html>`_ puedes encontrar un ejemplo interactivo y visual de una CNN para  reconocimiento de dígitos.


.. note::  No te preocupes si no entiendes al 100% todos los links o su teminología, pero para los videos se recomienda verlos un par de veces para comprender los conceptos, ya que es la base del aprendizaje.

Detección de Objetos
---------------------
De acuero con `wikypedia <Área relacionada con la visión artificial y el procesamiento de imagen que trata de detectar casos de objetos semánticos de una cierta clase (como humanos, edificios, o coches) en vídeos e imágenes digitales.​>`_
la detección de objetos es: Área relacionada con la visión artificial y el procesamiento de imagen que trata de detectar casos de objetos semánticos de una cierta clase (como humanos, edificios, o coches) en vídeos e imágenes digitales.​

Es diferente un problema de clasificación cómo:


.. figure:: img/fiat.jpg
    :width: 200px
    :align: center    

[#f1]_

Donde es una sola clase en toda la imagen; a un problema de reconocimiento y clasificación como:

.. figure:: img/or.png
    :width: 200px
    :align: left 

.. figure:: img/or1.png
    :width: 220px
    :align: center  



Que son varias instancias de varias clases en una sola imágen. Como podemos ver, para
el segundo ejemplo es necesario definir qué objeto se encuentra y que región ocupa
dentro de la imagen.
Algunas arquitecturas que se usan para problemas como el segundo ejemplo son:


* Region Based Object Detectors como R-CNN, Fast RCNN, Faster R-CNN, R-FCN, FPN You can learn a bit more 👁`here <https://medium.com/@jonathan_hui/what-do-we-learn-from-region-based-object-detectors-faster-r-cnn-r-fcn-fpn-7e354377a7c9>`_

Estas usan una ventana que mueven por toda la imagen, esta imagen de la ventana se ajusta a un tamaño fijo 
y a cada una se le aplica un clasificador. Para reducir el número de operaciones, se usan métodos
que proponen Regiones de Interés o  *Regions of Interest* (ROIs) o una red completa como *Region Proposal Network*
o RPN, que reducen el número de ventanas a analizar,
lo cuál se traduce en menor tiempo de entrenamiento. Pero para región se hacen *k* propuestas de región
por clase. El número de operaciones que se hacen sigue siendo elevado.

* 👁 `Single Shot Detectors como YOLO y SSD <https://medium.com/@jonathan_hui/what-do-we-learn-from-single-shot-object-detectors-ssd-yolo-fpn-focal-loss-3888677c5f4d>`_

Cómo se explica en el link, estas arquitecturas calculan al mismo tiempo un *boundary box* y la clase. Estos resultan ser buenos en procesamiento en tiempo real, pero tienenalgunos problemas
para detectar objetos o muy cercanos o muy lejanos.


Uno de los grandes problemas en detección de objetos y en general de Machine Learning,
es la selección del modelo. Esto se resuleve muchas veces de manera empírica o por
prueba y error. Vamos a tratar de implementar YOLO y SSD, sin dejar de tomar como opciones
otras arquitecturas.


Documentación YOLO y SSD:

* `Página oficial YOLO <https://pjreddie.com/darknet/yolo/>`_

* `Artículo YOLO <https://arxiv.org/abs/1506.02640>`_

* `Artículo SSD <https://arxiv.org/abs/1512.02325v5>`_

   
¿Cómo se implementan?
---------------------------
Primero debemos configurar nuestro ambiente de desarrollo. Cómo se explicó en la Introducción este debe 
ser implentado en Ubuntu Focal. Lo que ocupamos:

* `Anaconda <https://www.anaconda.com/>`_ : Aunque no es necesaria, es súper útil para crear ambientes con diferentes especificaciones. Además tiene otras herremientas para trabajar. Se pudieran usar otras herramientas como pipenv. 

* `Tensorflow <https://www.tensorflow.org/>`_ Es una plataforma que contiene herramientas, librerías y recursos que permiten a los desarrolladores introducirse al estado del arte en Machine Learning.​ La implementación de arquitecturas de redes neuronales es relativamente fácil. ​Con 3 líneas de código es posible agregar capas. Basta con cambiar las entradas (placeholders) para usar en otras aplicaciones.​

* `Keras <https://keras.io/>`_  es un API de alto nivel escrita en python para redes neuronales, permite trabajar por encima de Tensorflow. Ideal para hacer prototipos fáciles y rápidos.​ Usa el backend de tensorflow y tiene ya implementadas capas que son comunes en muchas arquitecturas​


**Hardware**

Es recomendable tener una tarjeta gráfica con poder computacional >=3.5 para el entrenamiento. 
Aunque se puede usar solo CPU, los tiempos de entrenamiento aumentan muy considerablemente.
Si se cuenta con tarjeta gráfica, estos son los requerimientos de hardware de acuerdo a la `página
oficial de Tensorflow <https://www.tensorflow.org/install/gpu#hardware_requirements>`_

* `Compute Capability Nvidia GPUs <https://developer.nvidia.com/cuda-gpus>`_


En resúmen Tensorflow tiene soporte para CPU y GPU, es mil vices más recomendable GPU, para la instalación 
de cualquiera de los dos se puede hacer por comandos pip o usando una imagen de docker. Nuevamente lo ideal
y en teoría más sencillo es con una imagen de docker, pues solo se tienen que instalar los drivers manualmente,

​

Instalación
===========

Brief Summary
-------------

Última actualización: 6/22/2019 with TensorFlow v1.13.1. 

Pripalmente está basado en
`el repositorio de EdjeElectronics <https://github.com/EdjeElectronics/TensorFlow-Object-Detection-API-Tutorial-Train-Multiple-Objects-Windows-10>`_
y
`el de Khaivdo <https://github.com/Khaivdo/How-to-train-an-Object-Detector-using-Tensorflow-API-on-Ubuntu-16.04-GPU>`__'s
repositories.

.. note:: El desarrollo se hizo con CPU, pues se contaba con una GPU antigua con poca capacidad de computo. Se anunciará que comandos pueden cambiar para diferente versión de Ubuntu o Tensorflow además de algunos links  de ayuda para la instalación y algunos posibles problemas que se prevean.Aquí se usó Tensorflow CPU 1.7


1. Anaconda
-------------------
Instalar los requerimientos:

::

    sudo apt-get install libgl1-mesa-glx libegl1-mesa libxrandr2 libxrandr2 libxss1 libxcursor1 libxcomposite1 libasound2 libxi6 libxtst6 -y

Descarga el archivo de instalación con estos comandos:

::

    cd  ~/Desktop
    wget https://repo.anaconda.com/archive/Anaconda3-2020.02-Linux-x86_64.sh
    chmod +x Anaconda3-2020.02-Linux-x86_64.sh 

Y ejecuta:

::

    sh Anaconda3-2020.02-Linux-x86_64.sh -y

Ahora que está instalado, puedes borrar el archivo:
::

    rm Anaconda3-2020.02-Linux-x86_64.sh

2. Create and set your environment
----------------------------------

Open a new terminal and it should appear *(base)* before your user name.

*I case it doesn't, run this commands:* :sub:`~` eval
"$(/home//anaconda3/bin/conda shell.bash hook) conda init :sub:`~` *In
case you use a different shell, replace shell.bash for shell.<
YourShell>*

Download the spec-list\_tf-cpu.txt file
`here <https://ugtomx-my.sharepoint.com/:f:/g/personal/de_gamasandoval_ugto_mx/EpCz_C7gow5Ai7OjD9TBcoABi6aGlIjGSsUvc4n5Gj3mdA?e=VbZKWV>`__:
Now let's create and activate our environment: :sub:`~` conda create
--name tf-cpu --file ~/Downloads/spec-list\_tf-cpu.txt conda activate
tf-cpu :sub:`~` Install this dependecies: :sub:`~` pip install Cython
pip install contextlib2 pip install pillow pip install lxml pip install
jupyter pip install matplotlib pip install pandas pip install
opencv-python pip install
"git+https://github.com/philferriere/cocoapi.git#egg=pycocotools&subdirectory=PythonAPI"
:sub:`~` Install tensorflow version 1.7 :sub:`~` pip install
tensorflow==1.7 :sub:`~` *You can propably use another version but some
lines of code might change, and you'll need to find its corresponding
API version*

3. Download repositories
------------------------

First create a directory on your Desktop :sub:`~` cd ~/Desktop mkdir
ObjectDetection :sub:`~` ### 3.3 `This
Repository <https://github.com/Daegas/CustumObjectDetection>`__

3.2 `Tensorflow Object Detection API <https://github.com/tensorflow/models>`__
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

There are several branches of the API they are targeted to different
tensorflow versions, since we installed version 1.7,
`here <https://github.com/tensorflow/models/tree/adfd5a3aca41638aa9fb297c5095f33d64446d8f>`__
is the corresponding branch. You have two option for download it: -
Directly from github (Click on Clone or Download button) and then
extract it on your ~/Desktop/ObjectDetection directory. - Or you can try
with these commands, which I saw works properly :sub:`~` cd
~/Desktop/ObjectDetection git clone https://github.com/tensorflow/models
cd models git reset --hard adfd5a3aca41638aa9fb297c5095f33d64446d8f
:sub:`~` *You basically download the current repository and then reset
to an old commit with its sha.*

3.3 `Model Zoo <https://github.com/tensorflow/models/blob/master/research/object_detection/g3doc/detection_model_zoo.md>`__
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

You can find a list of models, download and extract into
PretrainedModels. Here will use
`ssd\_inception\_v2\_coco <http://download.tensorflow.org/models/object_detection/ssd_inception_v2_coco_2018_01_28.tar.gz>`__
Finally this is how ObjectDetection should look

::

                                                    ADD IMAGE

4. Compile Protobufs
--------------------

Protobuf is a way to share data among applications, a little bit like
what JSON does. Is used by tensorflow to configure models and training
parameters and is implemented for several languages. So we need to
compile it for python. :sub:`~` cd
~/Desktop/ObjectDetection/models/research protoc
object\_detection/protos/\*.proto --python\_out=. :sub:`~` This creates
a name\_pb2.py file from every name.proto file in the
/object\_detection/protos folder.

**(Note: TensorFlow occassionally adds new .proto files to the folder.
If you get an error saying ImportError: cannot import name
'something\_something\_pb2' , you may need to update the protoc command
to include the new .proto files.)**

5. PYTHONPATH
-------------

For running, you need to specify where it gathers the data. So add
models/research to your PYTHONPATH. You'll need eat for each new
terminal, you could add it to your .bashrc file which is in /home and
appear by pressing ``Ctrl``\ +\ ``h`` but you'll need to replace the
``pwd`` for the absolute path to models/research.

::

    cd ~/Desktop/ObjectDetection/models/research/
    export PYTHONPATH=$PYTHONPATH:`pwd`:`pwd`/slim

6. Test
-------

There are 2 ways to test your installation ### Easy Just run: :sub:`~`
cd ~/Desktop/ObjectDetection/models/research/ python
object\_detection/builders/model\_builder\_tf1\_test.py :sub:`~` Looks
like this: ADD IMAGE

Explained
~~~~~~~~~

::

    cd ~/Desktop/ObjectDetection/models/research/object_detection
    jupyter notebook object_detection_tutorial.ipynb

If it doesn't opens directly the notebook, click on the link that
appears on your terminal and open the notebook
object\_detection\_tutorial.ipynb listed.

::

                                                    ADD IMAGE

*This section is from
`Edje <https://github.com/EdjeElectronics/TensorFlow-Object-Detection-API-Tutorial-Train-Multiple-Objects-Windows-10>`__*

This opens the script in your default web browser and allows you to step
through the code one section at a time. You can step through each
section by clicking the “Run” button in the upper toolbar. The section
is done running when the “In [ \* ]” text next to the section populates
with a number (e.g. “In [1]”).

(Note: part of the script downloads the ssd\_mobilenet\_v1 model from
GitHub, which is about 74MB. This means it will take some time to
complete the section, so be patient.)

Once you have stepped all the way through the script, you should see two
labeled images at the bottom section the page. If you see this, then
everything is working properly! If not, the bottom section will report
any errors encountered. See the
`Appendix <https://github.com/EdjeElectronics/TensorFlow-Object-Detection-API-Tutorial-Train-Multiple-Objects-Windows-10#appendix-common-errors>`__
for a list of errors I encountered while setting this up.

**Note: If you run the full Jupyter Notebook without getting any errors,
but the labeled pictures still don't appear, try this: go in to
object\_detection/utils/visualization\_utils.py and comment out the
import statements around lines 29 and 30 that include matplotlib. Then,
try re-running the Jupyter notebook.**



.. rubric:: Footnotes

.. [#f1] https://thumbs.dreamstime.com/b/old-fiat-500-1-13471810.jpg