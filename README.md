# Custom Object Detection with Tensorflow 1.7 API on Ubuntu 18

## Brief Summary
*Last updated: 6/22/2019 with TensorFlow v1.13.1*
*Mainly based on [EdjeElectronics](https://github.com/EdjeElectronics/TensorFlow-Object-Detection-API-Tutorial-Train-Multiple-Objects-Windows-10)'s and [Khaivdo](https://github.com/Khaivdo/How-to-train-an-Object-Detector-using-Tensorflow-API-on-Ubuntu-16.04-GPU)'s repositories.*
*This repository attempts to make it work with specific Tensorflow CPU version 1.7 and its corresponding API*

## 1. Install Anaconda
*Is useful for version management*

Install the previous requirements:
```
sudo apt-get install libgl1-mesa-glx libegl1-mesa libxrandr2 libxrandr2 libxss1 libxcursor1 libxcomposite1 libasound2 libxi6 libxtst6 -y
```
Get the installation .sh  file by running this commands:
```
cd  ~/Desktop
wget https://repo.anaconda.com/archive/Anaconda3-2020.02-Linux-x86_64.sh
chmod +x Anaconda3-2020.02-Linux-x86_64.sh 
```
Execute it:
```
sh Anaconda3-2020.02-Linux-x86_64.sh -y
```
And if you pleased delete the it:
```
rm Anaconda3-2020.02-Linux-x86_64.sh
```
## 2. Create and set your environment

Open a new terminal and it should appear (base) before your user name. 

*I case it doesn't, run this commands:*
~~~
eval "$(/home/<USER>/anaconda3/bin/conda shell.bash hook)
conda init
~~~
*In case you use a different shell, replace shell.bash for shell.< YourShell>* 

Download the spec-list_tf-cpu.txt file [here](https://ugtomx-my.sharepoint.com/:f:/g/personal/de_gamasandoval_ugto_mx/EpCz_C7gow5Ai7OjD9TBcoABi6aGlIjGSsUvc4n5Gj3mdA?e=VbZKWV):
Now let's create and activate  our environment:
~~~
conda create --name tf-cpu --file ~/Downloads/spec-list_tf-cpu.txt
conda activate tf-cpu
~~~
Install this dependecies:
~~~
pip install Cython
pip install contextlib2
pip install pillow
pip install lxml
pip install jupyter
pip install matplotlib
pip install pandas
pip install opencv-python
pip install "git+https://github.com/philferriere/cocoapi.git#egg=pycocotools&subdirectory=PythonAPI"
~~~
Install tensorflow version 1.7
~~~
pip install tensorflow==1.7
~~~
*You can propably use another version but some lines of code might change, and you'll need to find its corresponding API version* 

## 3. Download repositories
First create a directory on your Desktop
~~~
cd ~/Desktop
mkdir ObjectDetection
~~~
### 3.3 [This Repository](https://github.com/Daegas/CustumObjectDetection)

### 3.2 [Tensorflow Object Detection API](https://github.com/tensorflow/models) 
There are several branches of the API they are targeted to different tensorflow versions, since we installed version 1.7, [here](https://github.com/tensorflow/models/tree/adfd5a3aca41638aa9fb297c5095f33d64446d8f) is the corresponding branch. You have two option for download it:
- Directly from github (Click on Clone or Download button) and then extract it on your ~/Desktop/ObjectDetection directory.
- Or you can try with these commands, which I saw  works properly
~~~
cd ~/Desktop/ObjectDetection
git clone https://github.com/tensorflow/models
cd models
git reset --hard adfd5a3aca41638aa9fb297c5095f33d64446d8f
~~~
*You basically download the current repository and then reset to an old commit with its sha.*

### 3.3 [Model Zoo](https://github.com/tensorflow/models/blob/master/research/object_detection/g3doc/detection_model_zoo.md) 
You can find a list of models, download and extract into PretrainedModels. Here will use [ssd_inception_v2_coco](http://download.tensorflow.org/models/object_detection/ssd_inception_v2_coco_2018_01_28.tar.gz)
Finally this is how ObjectDetection should look

													ADD IMAGE


## 4. Compile Protobufs
Protobuf is a way to share data among applications, a little bit like what JSON does. Is used by tensorflow to configure models and training parameters and is implemented for several languages. So we need to compile it for python. 
~~~
cd ~/Desktop/ObjectDetection/models/research
protoc object_detection/protos/*.proto --python_out=.
~~~
This creates a name_pb2.py file from every name.proto file in the /object_detection/protos folder.

**(Note: TensorFlow occassionally adds new .proto files to the \protos folder. If you get an error saying ImportError: cannot import name 'something_something_pb2' , you may need to update the protoc command to include the new .proto files.)**

##  5. PYTHONPATH
For running, you need to specify where it gathers the data. So add models/research to your PYTHONPATH. You'll need eat for each new terminal, you could add it to your .bashrc file which is in /home and appear by pressing ```Ctrl```+```h```  but you'll need to replace the `pwd` for the absolute path to models/research.
```
cd ~/Desktop/ObjectDetection/models/research/
export PYTHONPATH=$PYTHONPATH:`pwd`:`pwd`/slim
```
## 6. Test
There are 2 ways to test your installation
### Easy
Just run:
~~~
cd ~/Desktop/ObjectDetection/models/research/
python object_detection/builders/model_builder_tf1_test.py
~~~
Looks like this:
									ADD IMAGE			

### Explained
~~~
cd ~/Desktop/ObjectDetection/models/research/object_detection
jupyter notebook object_detection_tutorial.ipynb
~~~
If it doesn't opens directly the notebook, click on the link that appears on your terminal and open the notebook object_detection_tutorial.ipynb listed.

													ADD IMAGE
*This section is from [Edje](https://github.com/EdjeElectronics/TensorFlow-Object-Detection-API-Tutorial-Train-Multiple-Objects-Windows-10)*


This opens the script in your default web browser and allows you to step through the code one section at a time. You can step through each section by clicking the “Run” button in the upper toolbar. The section is done running when the “In [ * ]” text next to the section populates with a number (e.g. “In [1]”).

(Note: part of the script downloads the ssd_mobilenet_v1 model from GitHub, which is about 74MB. This means it will take some time to complete the section, so be patient.)

Once you have stepped all the way through the script, you should see two labeled images at the bottom section the page. If you see this, then everything is working properly! If not, the bottom section will report any errors encountered. See the  [Appendix](https://github.com/EdjeElectronics/TensorFlow-Object-Detection-API-Tutorial-Train-Multiple-Objects-Windows-10#appendix-common-errors)  for a list of errors I encountered while setting this up.

**Note: If you run the full Jupyter Notebook without getting any errors, but the labeled pictures still don't appear, try this: go in to object_detection/utils/visualization_utils.py and comment out the import statements around lines 29 and 30 that include matplotlib. Then, try re-running the Jupyter notebook.**



