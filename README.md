# What is the purpose of this repo?
This repo hosts the custom cloudbees jenkins agent image to be deployed on Openshift.
# How to build a docker image.
To build the image, make sure you are in the root directory in where the Dockerfile is located. Then build and tag it using the following command: `docker build -t tougemasta/cloudbees:latest .`

Once the image has been built, push it to the tougemasta dockerhub account repository using this command: `docker push tougemasta/cloudbees:latest`
