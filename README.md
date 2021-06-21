## Overview
The objectif is to develop and package, in a running docker container, a classification application for MNIST data.

##  Architecture

All the architecture is encapsulated in a [docker](https://www.docker.com/) container. It allows to any user to install the application, upload an image from the test_dataset MNIST and obtain the prediction of the number written on (prediction returned in a json file).

A simple web inteface has been developped (Flask framework) allowing the user to select the files used for prediction.

##  Requirements

* [Docker Engine](https://docs.docker.com/install/) (version 20.10.6)
* 2.5 GB de RAM

##  Setup
In order to launch the creation of the Docker image, follow the instructions below :

- Install [docker](https://www.docker.com/) (version 20.10.6) and run the application.

- Open a shell in the directory where the file ```Dockerfile``` is saved and run the command :
```
    $ docker build -t mnist-prediction:latest .
```
Wait until the process succeded in the creation of the Docker image.

- Run the command to start the container :
```
    $ docker run -d -p 5000:5000 mnist-prediction
```

- Open your browser and use the following adress :
```
    http://localhost:5000/
```

- Use the Form to select your files and obtain your prediction ! (10 images from the test dataset are available in the folder images_test)

<p align="center">
<img src="img/app.JPG" alt="drawing" width="500"/>
</p>

##  Workflow

At the root of the project, we find the file ```backend.py``` containing the classifier code, the pipeline preprocessing and the training method. 
The Flask application is coded in the file ```app.py```. You find also the Dockerfile (with the requirements) for the creation of the Docker image.

- The Docker container launches the Flask application, accessible with the following command in your web browser :
```
    http://localhost:5000/
```
- The File Selection Form is available and will send the images selected to the server.
- The Classifier (under the ```backend.py``` file) is then called and realize the prediction.
- The server returns the prediction in a json file.

## Data used
Classification model trained (accuracy on test dasaset 98.6%) : SVM deg 4 polynomial + deskewing preprocessing  
Data available on the website http://yann.lecun.com/exdb/mnist/  
Train data : train-images-idx3-ubyte.gz + train-labels-idx1-ubyte.gz  
Test data : t10k-images-idx3-ubyte.gz + t10k-labels-idx1-ubyte.gz  

##  References
- https://stackoverflow.com/questions/40427435/extract-images-from-idx3-ubyte-file-or-gzip-via-python
- https://stackoverflow.com/questions/43577665/deskew-mnist-images
