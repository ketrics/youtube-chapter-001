# How to deploy a containerized application to DigitalOcean's Droplet

Here I will leave you all the commands used in the video to deploy the Jupyter DataScience Notebook .

I will also leave here some interesting articles:

What AWS lambdas functions and how they are executed?

https://aws.amazon.com/blogs/compute/container-reuse-in-lambda/

Why should you use microservices and containers?

https://developer.ibm.com/articles/why-should-we-use-microservices-and-containers/

Containers as the foundation for DevOps collaboration

https://docs.microsoft.com/en-us/dotnet/architecture/containerized-lifecycle/docker-application-lifecycle/containers-foundation-for-devops-collaboration


## Login as root into your Droplet using its public IP
    ssh root@<YOUR DROPLET IP>

## Create a user to avoid using the root user and git it privileges
    adduser cristian
    usermod -aG sudo cristian && usermod -aG docker cristian

## Create a directory to put your custom app files
    mkdir /apps && chown cristian /apps && chgrp cristian /apps

## Change to the new user
    su cristian

## Add your public key to your new user's authorized keys
    cd /home/cristian && mkdir ~/.ssh && chmod 700 ~/.ssh
    nano ~/.ssh/authorized_keys

    chmod 600 ~/.ssh/authorized_keys
    sudo systemctl reload sshd

    exit
    exit

## Login as your own user
    ssh cristian@<YOUR DROPLET IP>

    cd /apps
    mkdir -p jupyter/notebooks

## Run your first Container Application

    docker run -d --rm -p 8888:8888 --name jupyter -v /apps/jupyter/notebooks:/home/jovyan/work jupyter/datascience-notebook

### Flags explanation
    -d      is for detached mode
    --rm    is to automatically remove this container after it has stopped
    -p      is to map a host port to a container port
    --name  is to give the container a name so we can reference to it easier
    -v      is to map a host directory to a container directory in order to persist the changes made inside the container


## Get Jupyter token to connect
    docker exec jupyter jupyter notebook list


