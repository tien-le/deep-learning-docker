&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;![Getting Started With Docker](https://github.com/ajaymache/getting-started-with-docker/blob/master/misc/images/DockerLogo.png)

## Introduction
This repository aims at getting you started with [docker](https://www.docker.com/) by setting up environment for machine learning/deep learning libraries and frameworks.

### What is docker?
- Docker is the world’s leading software container platform. Developers use Docker to eliminate “works on my machine” problems when collaborating on code with co-workers.

- Operators use Docker to run and manage apps side-by-side in isolated containers to get better compute density. 

- Enterprises use Docker to build agile software delivery pipelines to ship new features faster, more securely and with confidence for both Linux and Windows Server apps.

### What is an image?
- An image is a lightweight, stand-alone, executable package that includes everything needed to run a piece of software, including the code, a runtime, libraries, environment variables, and config files.

### What is a container?
- A container is a runtime instance of an image — what the image becomes in memory when actually executed. It runs completely isolated from the host environment by default, only accessing host files and ports if configured to do so.

- Using containers, everything required to make a piece of software run is packaged into isolated containers. Unlike VMs, containers do not bundle a full operating system - only libraries and settings required to make the software work are needed.

- This makes for efficient, lightweight, self-contained systems and guarantees that software will always run the same, regardless of where it’s deployed. To learn more about containers click [here](https://www.docker.com/what-container).

## Installing docker
- Install the docker application following the installation guide for your platform from [here](https://docs.docker.com/engine/installation/)

## Setting up the environment
- The Docker Engine client runs natively on **Linux**, **macOS**, and **Windows**. By default, these clients connect to a local Docker daemon running in a virtual environment managed by Docker, which provides the required features to run Linux-based containers within OS X or Windows, or Windows-based containers on Windows.

- The steps mentioned below are performed with the docker application installed on **OSX (macOS)**. Following the steps mentioned below, you should be able to setup a customized docker image and push to [dockerhub](https://hub.docker.com/).

### Starting with a base image
- While making a custom docker image most of the times you will encounter that one usually starts with a base image. Here we will be using **ubuntu** as our base image.

- Please note that we **do not** have to make the ubuntu image from scratch since its already been officially made by the community and we can use the same image as the starting point or base for creating our own image.

- To get **ubuntu** as the base image from the public repository on dockerhub do the following steps:

  **1.** Open terminal
  
  **2.** To check if docker daemon is running type the command ```docker version``` in the terminal. You should see something like as shown in the snapshot below:
     
  <p align="center">
  <img src="https://github.com/ajaymache/getting-started-with-docker/blob/master/misc/images/Screen%20Shot%202017-07-31%20at%207.42.14%20PM.png">
  </p>
     
    If you get an error make sure your docker application is running by looking for the whale icon in the upper task bar as shown in the snapshot below:
     
  <p align="center">
  <img src="https://github.com/ajaymache/getting-started-with-docker/blob/master/misc/images/Screen%20Shot%202017-07-31%20at%207.53.48%20PM.png">
  </p>

     
  **3.** Proceed from here only if your docker is running as mentioned above. Since we have started the docker application for the      first time we do not have any images yet. Lets confirm that by typing the command ```docker images``` in the terminal. You will notice that nothing is listed which confirms that we do not have any images.
      
  **4.** To get the ubuntu image as the base image type the command ```docker pull ubuntu``` in the terminal. This might take a while depending on your internet speed because it is fetching the image from the dockerhub which is  available publicy for use. You should see the download progressing as shown below:
     
  <p align="center">
  <img src="https://github.com/ajaymache/getting-started-with-docker/blob/master/misc/images/Screen%20Shot%202017-08-01%20at%208.17.52%20PM.png">
  </p>
     
  **5.** Now type ```docker images``` as mentioned in step 3 to see the list of images you have downloaded on your machine. You should see something like as shown in the snapshot below:
  
  <p align="center">
  <img src="https://github.com/ajaymache/getting-started-with-docker/blob/master/misc/images/Screen%20Shot%202017-08-01%20at%208.21.01%20PM.png">
  </p>
  
### Running a container from an image
- In this section we will spin up a container from the base image **ubuntu** which we just pulled from the dockerhub.

  **1.** To run the **ubuntu** image type the command ```docker run -it ubuntu``` in the terminal. Note how the terminal changes pointing to the container which we spinned up just now as shown below:

  <p align="center">
  <img src="https://github.com/ajaymache/getting-started-with-docker/blob/master/misc/images/Screen%20Shot%202017-08-01%20at%208.21.01%20PM.png">
  </p>
  
  
  **2.** In order to install the required machine learning/deep learning libraries and frameworks we frist need some tools since the ubuntu image we pulled is very basic and essentially comes only with the kernel and hence it is light weight which is the basically the whole idea of docker. Execute the following commands sequentially one after the other in the terminal to get the required tools.
  
  ```bash
  apt-get update
  ```
  
   This command will get the latest updates if any. Below is the output after running this command in the terminal:
  
  <p align="center">
  <img src="https://github.com/ajaymache/getting-started-with-docker/blob/master/misc/images/Screen%20Shot%202017-08-01%20at%208.26.12%20PM.png">
  </p>
  
  ```bash
  apt-get install -y wget
  ```
  
  This command will get the **GNU Wget** which is a open source software package for retrieving files using HTTP, HTTPS and FTP.
  
  ```bash
  apt-get install -y bzip2
  ```
  
  This command will get the **bzip2** package which will be required to decompress some of the **Anaconda** files which we will see in the next section.

### Installing Anaconda
- To avoid installing every library individually we will download and install Anaconda 4.2 with Python 3.5.

  **1.** To create a **Downloads** folder in the **home** directory type ```mkdir home/Downloads``` in the terminal.
 
  **2.** Navigate to this folder by typing ```cd home/Downloads``` in the terminal.
 
  **3.** To get Anaconda 4.2 with Python 3.5 archive file type ```wget https://repo.continuum.io/archive/Anaconda3-4.2.0-Linux-x86_64.sh``` in the terminal. This might take a while since the file is about **~385 MB**.
  
- After downloading the Anaconda file as explained in the previous section follow the steps below to complete the installation.

  **1.** To initiate the installation type ```bash ./Anaconda3-4.2.0-Linux-x86_64.sh``` in the terminal and hit enter. You will be prompted to read and agree the **license terms and conditions**. keep pressing enter until you are asked to accept the license terms. Type **yes** and hit enter to proceed.
  
  **2.** After you accept the license terms above you will be prompted with the message __*Anaconda3 will be now installed into the root location:*__ ```/root/anaconda3```, we will go with the default settings and hence **press enter** to proceed. This might take a while to install and you can see the logs in the console.
  
  **3.** In the end you will be asked if you would like to append the Anaconda3 install location to **PATH** in your ```/root/.bashrc```. Type **yes** and hit enter to complete the installation.
  
  :warning: At this point the installation for **Anaconda** is complete but for the changes to come into effect we need to open a new terminal. One way is we can stop the running container and restart it in a new terminal window or we could simply attach the running container to a new terminal session. To keep it simple for this tutorial we will go with the first option.
  
  **4.** To stop the container type ```exit``` in the terminal and you will notice the terminal directory changes from ```root@....``` to your **home** directory.
  
### Restarting the stopped container
- To restart the stopped conatiner we need the **CONTAINER ID**. Follow the steps below to obtain the **CONTAINER ID** and restart the container.

  **1.** To get the **CONATINER ID** type ```docker ps -a``` in the terminal. You will be listed with the **CONTAINER ID** and some more information about the container regarding when it was created, stopped etc. Copy this **CONTAINER ID**.
  
  <p align="center">
  <img src="https://github.com/ajaymache/getting-started-with-docker/blob/master/misc/images/Screen%20Shot%202017-08-01%20at%2010.17.41%20PM.png">
  </p>
  
  **2.** To start the container type ```docker container start -i CONTAINER ID``` in the terminal. This will again restart the container which we stopped before and you can verify it by looking at terminal which will be pointing to ```root@....```.
  
  :warning: Do not forget to update the **CONTAINER ID** keyword with the _**actual container id**_ in **step 2** above while starting the container.

