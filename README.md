# Data Splitter

This is for splitting document uuids as test-{timestamp}.txt and train-{timestamp}.txt according to resources uuids.

##Built a docker image
```
docker build -t docker.omnius.com/splitter:1.0.0 .
```
To be able to push the image with docker push you need to be authorized to upload images on the omni:us docker registry.
##Prerequisites
* PYTHON You need to have a python dev environment with python >= 3, pip3, virtualenv

##ENV Variables
* MOUNTED_FOLDER is a directory where resource uuids exist
* OUTPUT_FOLDER is a directory where split script extracts data
* RESOURCE_KEYS is a comma separated value where document uuids exist
* TEST_SIZE is a float value that specifies test data percentage (default 0.20)
* TIMESTAMP is for creation of txt files
##Usage
###Injecting to cluster
* There is a helm cart for splitting-service;
```
helm tiller run helm upgrade --install splitter omnius/splitter --version 1.0.0 --set CUSTOMERNAME=trainer --set ENV=qa --set configmapvalues.RESOURCE_KEYS={{resources keys}} --set configmapvalues.TIMESTAMP={{timestamp}}
```
* After injection, Kubernetes job creates 2 txt files inside OUTPUT_FOLDER
  * One of them is for test with format `test-{timestamp}.txt` as an example: `test-1553272487.txt`
  * Other one is for train with format `train-{timestamp}.txt` as an example: `train-1553272487.txt`
# Project Steering Committee (PSC)
The PSC provides guidance, direction and control over this software project.
 
The members are:
* Berat Caner Özer [leader]
* Vasanth Bathrinarayanan
 
The PSC is accountable and responsible to make the following processes smooth, enjoyable and productive:
* Code review
* Release process and artifact distribution (as binaries and/or docker images)
* Continuous integration
* Technical documentation and guidance to new contributors
