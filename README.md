# Introduction to Metagenomics

This repository contains the 

- Lecture slides
- codesandbox devfiles and dockerfile
- Tutorial instructions


## How to install outside of codesandbox
Using docker (place Docker file in current directory):
```
docker build -t metagenomicstutorial:latest .
docker run -it metagenomicstutorial:latest
```
<br>

Using singularity:
```
#build the image using docker
docker build -t metagenomicstutorial:latest .
#export it
docker save metagenomicstutorial:latest >  metagenomicstutorial.tar
#build singularity image
singularity build metagenomicstutorial.sif docker-archive://metagenomicstutorial.tar
#run container
singularity run metagenomicstutorial.sif
```
