## Ubuntu Desktop Bioinformatics Docker Images

- Beginner-friendly - best-in-class software preinstalled and a familiar Desktop environment.
- Send a Docker image and take a look around without typing 'cd' 100 times.
- Customize via apt, bioconductor, CRAN, etc.
- Reproducible science*

Released [Desktop Images](https://hub.docker.com/repository/registry-1.docker.io/windybasket/public/tags?page=1) including base and single-cell RNA sequencing Images at the link. We show the utility of the images by modifying the base image into a single-cell RNA (ScRNA) sequencing image and an image based on Viraltrack.

\* *may vary*

## Getting Started

We only need to install Docker and download the accompanying Docker Image once on our computer to run images. To do this:
[Install Docker](https://docs.docker.com/get-docker/)

On Mac, start the Docker Desktop app in your app folder. There should be a Docker icon in the top right (whale) on successful startup.
On Windows, start the Docker Desktop app by searching in the start bar.  There should be a Docker icon in the bottom right (whale) on successful startup.

Open up a terminal and type:

`sudo docker pull windybasket/public:base_1.01` (Gets the accompanying Docker Image)

Now we type:

`sudo docker run -p 6080:80 -v /dev/shm:/dev/shm windybasket/public:base_1.01` (start the Docker virtual computer)

[Go to the Desktop](http://127.0.0.1:6080/), open up a web browser and go to http://127.0.0.1:6080/

## Installed Tools
Ubuntu Desktop, Firefox, Git, Curl and Wget, Nano, Firefox, Htop
Python3, Pip3, Miniconda, pycharm (run with `./pycharm.sh`)
R 4.0, Rstudio, devtools (for R)
Samtools
SRA Toolkit
Igv

## Highly Customizable

Using the base Docker image and installing further software simplifies generating custom images for specific use cases. A second Image was generated with additional single-cell rna sequencing software installed, demonstrating the utility of the images. Bioinformatic software is highly diverse and changes rapidly; for this reason we install software to install software.

Example software installation: SRA-Toolkit

Installation is standard procedure for Ubuntu not in apt:

[Download for Ubuntu](https://ncbi.github.io/sra-tools/install_config.html)

Go to Downloads file and unzip: `tar -xvf sratoolkit.2.10.8-ubuntu64.tar.gz`

Place sratoolkit.2.10.8-ubuntu64 folder in tools folder `/root/tools`

Edit and source bash profile:

`sudo nano ~/.profile`
append to end of file and save (cntrl+x):
`export PATH=$PATH:/root/tools/sratoolkit.2.10.8-ubuntu64/bin`
source edited profile: `source ~/.profile`

Specific to sratoolkit:

run `vdb-config -i`

## Common Docker Operations

###Copy files from the local machine to the virtual machine:

On your local machine open up a new terminal. Next we list running docker images:

`sudo docker ps`

We get something back like:

CONTAINER ID        IMAGE                           COMMAND             CREATED             STATUS                 PORTS                  NAMES
b16ef82f8152        windybasket/public:base   "/startup.sh"       2 hours ago         Up 2 hours (healthy)   0.0.0.0:6080->80/tcp   clever_keller

note NAMES: clever_keller

The docker cp command is similar to cp for linux and follows the syntax: `sudo docker cp wherefileis NAMES:wherefilegoes`

so if our file is on our local machine at `~/Downloads/files`, and we wanted to put it on our desktop in the docker image, we would type:

`sudo docker cp ~/Downloads/files clever_keller:/root/Desktop`


Save/share a Docker Image on your online account with Docker push
Scale up and SSH into a machine on the cloud or x11 forward the desktop (may be affected by lag).

First example: copy files from the local machine into the Docker Images

For this example, we copy in cellranger to our tools folder as if we're installing/updating it.
First get the name of the Docker container

`sudo docker ps`

CONTAINER ID        IMAGE                     COMMAND             CREATED             STATUS                   PORTS                  NAMES
545c0ce1e2aa        windybasket/bio:base   "/startup.sh"       2 minutes ago       Up 2 minutes (healthy)   0.0.0.0:6080->80/tcp   brave_clarke

Next we copy our files from where they are on our local machie to where they should be in our Docker Image:

`sudo docker cp ~/Downloads/cellranger-4.0.0/ brave_clarke:/root/Desktop/`



List Docker Images on your local machine (used for 'docker push,pull,run')
`sudo docker image ls`

List Running Docker Containers on your local machine (used for 'docker cp')
`sudo docker ps`





Run a Docker Image
`docker run -p 6080:80 -v /dev/shm:/dev/shm windybasket/bio:base`

or more generally:
`docker run -p 6080:80 -v /dev/shm:/dev/shm user/build:tag`

Save your docker on Docker's website
`sudo docker ps`

docker commit CONTAINER_ID yourImage
`docker commit fbe973c7d5fc windybasket/bio:base`
`docker push windybasket/bio:base`

Create a new docker image from an existing one (if you customized an image and want to 'save as'):
`docker commit -p -a "author_here" -m "your_message" bd91ca3ca3c8 name_of_new_image`

sudo docker image ls
number of the image id you want to copy, name of what you want to have named
sudo docker tag 24572082869c windybasket/bio:single_cell_1
sudo docker push windybasket/bio:single_cell_1


trash is in ~/.local/share/Trash/files
sudo docker commit a19d55acb79a windybasket/bio:viraltrack
docker tag local-image:tagname new-repo:tagname
docker push new-repo:tagname
