## Ubuntu Desktop Bioinformatics Docker Images

- Beginner-friendly - hit the ground running and develop with best-in-class software and a familiar Desktop environment.
- Want to send all your work to a friend? Send them the Docker container and they can take a look around without typing 'cd' 100 times.
- Customize with ease via apt, bioconductor, CRAN, etc.
- Don't worry about blowing up your computer, work in a container.
- Reproducible science*

\* *may vary*

## Getting Started
We only need to install Docker and download the accompanying Docker Image once on our computer to run images. To do this:
[Get Docker](https://docs.docker.com/get-docker/)

Get the accompanying Docker Image:
`docker pull windybasket/bio:base`

## Run Docker
docker run -p 6080:80 -v /dev/shm:/dev/shm windybasket/bio:base
[Go to the Desktop](http://127.0.0.1:6080/)

## Installed Tools
Ubuntu Desktop, Git, Curl and Wget, Htop, Nano, Firefox
Python3, Pip3, Miniconda
R, Rstudio, devtools (for R)
Samtools
SRA Toolkit
Igv

## Some Docker Commands
We already know how to get a Docker Image and run it, but we can also:
Copy files from the virtual machine to your local machine with Docker cp
Save/share a Docker Image on your online account with Docker push

## Highly Customizable
Using the base Docker image and installing further software simplifies generating custom images for specific use cases. A second Image was generated with additional single-cell rna sequencing software installed to draw figures, demonstrating the utility of the images.
