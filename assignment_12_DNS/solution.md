# Docker, Nextflow & Singularity

## Uploading an image to Docker

### Authentication
1. Create an account on [docker hub](https://hub.docker.com/)
2. From your terminal, authenticate the docker application using `docker login`, this will require your credentials that your obtained in the previous step.

### Preparing your image for uploading
Incase you have pending changes or would like to make changes to your image, do so then run the following steps:
1. Obtain the container IDs `docker ps -a`
2. Commit your changes to a new image `docker commit [CONTAINER ID] [IMAGE NAME]`
3. Confirm that the image has been updated `docker images`, you should see your new image there.
4. (optional) Tag your image `docker tag SOURCE_IMAGE[:TAG] TARGET_IMAGE[:TAG]`

###  Pushing your image to docker
To share your image with other docker users, you need to upload it to docker hub, to do that run the following steps:
1. Push your image `docker push [IMAGE NAME]`
2. Check docker hub to see whether the changes have reflected

## Working with Singularity

### Building containers from existing ones
To work with an existing container your can download it to your local machine using:
```bash
sudo singularity build lolcow.simg library://sylabs-jms/testing/lolcow
```
Docker Hub containers can also be used by changing the URL as follows:
```bash
sudo singularity build lolcow.sif docker://godlovedc/lolcow
```

### Building a container from scratch
Singularity definition files can be used as a target when building containers. One can follow the following steps to build a container from a definition file:
1. Create a singularity definition file and save it as a `.def` file
```bash
Bootstrap: docker
From: ubuntu:16.04

%post
    apt-get -y update
    apt-get -y install fortune cowsay lolcat

%environment
    export LC_ALL=C
    export PATH=/usr/games:$PATH

%runscript
    fortune | cowsay | lolcat
```
2. Build the container from the `.def` file
```bash
sudo singularity build lolcow.sif lolcow.def
```

### Running the container
One can execute command from within the container for example we can run the following command in our container:
```bash
singularity exec lolcow.sif cowsay "Hello Singularity"
```

### Running the container interactively
To work within the container's shell one can run the following command:
```bash
singularity shell lolcow.sif
# Type other commands now in the container's shell ...
```

## Running Nextflow from GitHub
To allow pipeline sharing Nextflow supports running pipelines from code hosting platforms such as GitHub and BitBucket.

### Running a pipeline from GitHub
To run a pipeline from GitHub pass the name of the repository or its URL to the `nextflow run` command e.g:
```bash
# GitHub repository name
nextflow run githubname/mypipeline
# URL
nexflow run https://github.com/githubname/mypipeline
```
This will download the repo to your `$HOME/.nextflow` directory and execute the pipeline.

### Switching branches
To run a pipeline on a different branch use the `-r` option as shown below:
```bash
# GitHub repository name
nextflow run githubname/mypipeline -r myotherbranch
# URL
nexflow run https://github.com/githubname/mypipeline -r myotherbranch
```

### Updating the repository
To update the downloaded repository use the `pull` command:
```bash
# GitHub repository name
nextflow pull githubname/mypipeline
# URL
nexflow pull https://github.com/githubname/mypipeline
```