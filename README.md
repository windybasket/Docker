## Ubuntu Desktop Bioinformatics Docker Images

- Beginner-friendly - hit the ground running and develop with best-in-class software and a familiar Desktop environment.
- Want to send all your work to a friend? Send them the Docker container and they can take a look around without typing 'cd' 100 times.
- Customize with ease via apt, bioconductor, CRAN, etc.
- Don't worry about blowing up your computer, work in a container.
- Reproducible science*

Released ![Desktop Images](https://hub.docker.com/repository/docker/windybasket/bio/tags?page=1) including base and single-cell RNA sequencing Images at the link. We show the utility of the images by modifying the base image into a single-cell RNA (ScRNA) sequencing image, and use the ScRNA image to write a published paper including formatting, from data housed in the NCBI Sequence Read Archive (SRA).

\* *may vary*

## Getting Started

We only need to install Docker and download the accompanying Docker Image once on our computer to run images. To do this:
[Install Docker](https://docs.docker.com/get-docker/)

On Mac, start the Docker Desktop app in your app folder. There should be a Docker icon in the top right (whale) on successful startup.
On Windows, start the Docker Desktop app by searching in the start bar.  There should be a Docker icon in the bottom right (whale) on successful startup.

Open up a terminal and type:

`docker pull windybasket/bio:base` (Gets the accompanying Docker Image)

Now we type:

`docker run -p 6080:80 -v /dev/shm:/dev/shm windybasket/bio:base` (start the Docker virtual computer)

[Go to the Desktop](http://127.0.0.1:6080/), open up a web browser and go to http://127.0.0.1:6080/

## Installed Tools
Ubuntu Desktop, Firefox, Git, Curl and Wget, Nano, Firefox, Htop
Python3, Pip3, Miniconda
R 4.0.0, Rstudio, devtools (for R)
Samtools
SRA Toolkit
Igv

## Some Docker Commands
We already know how to get a Docker Image and run it, but we can also:
Copy files from the virtual machine to your local machine with Docker cp
Save/share a Docker Image on your online account with Docker push


## Highly Customizable

Using the base Docker image and installing further software simplifies generating custom images for specific use cases. A second Image was generated with additional single-cell rna sequencing software installed, demonstrating the utility of the images. Bioinformatic software is highly diverse and changes rapidly; for this reason we install software to install software.

Example software installation: SRA-Toolkit

Installation is standard procedure for Ubuntu not in apt:

[Download for Ubuntu](https://ncbi.github.io/sra-tools/install_config.html)

Go to Downloads file and unzip: `tar -xvf sratoolkit.2.10.8-ubuntu64.tar.gz`

Place sratoolkit.2.10.8-ubuntu64 folder in tools folder `/root/tools`

Edit and source bash profile:

`nano ~/.profile`
append to end of file and save (cntrl+x):
`export PATH=$PATH:/root/tools/sratoolkit.2.10.8-ubuntu64/bin`
source edited profile: `source ~/.profile`

Specific to sratoolkit:

run `vdb-config -i`

## Most Common Docker Commands
List Docker Images on your local machine
`sudo docker image ls`
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
