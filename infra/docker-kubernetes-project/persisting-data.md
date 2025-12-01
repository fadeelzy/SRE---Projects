##  DOCKER VOLUMES -   PERSIST DATA IN DOCKER
    When do need Docker Volumes ?
    What is a Docker Volumes ?
    3 Volume Types
    Docker Volumes in docker-compose file 
    Example 
        Databases
        Other Stateful Applications

## When do need Docker Volumes ?
      Container runs on the host 
        container /var/lib/mysql/data has virtual file system 
      Data is gone ! When restarting or removing the container

## What is a Docker Volumes ?
        Host        > /home/mount/data       > Host File System (physical)
        Container   > /var/lib/mysql/data    > Virtual File System
        We plug the physical path (folder/directory)  into the container
        Folder in physical host file system is mounted into the virtual file system of Docker
        Data gets automatically replicated 

## 3 Volume Types
    docker run -v /home/mount/data:/var/lib/mysql/data
                        HOST      : CONTAINER
    1: HOST VOLUMES
        You decide where on the host file system the referennce is made 
                        HOST MOUNT TO A CONTAINER

    2:  ANONYMOUS VOLUMES 
        docker run -v /var/lib/mysql/data
                        /var/lib/docker/volumes/random-hash/_data
          We're referencing container directory /var/lib/mysql/data
          For each container a folder is generated that gets mounted (Automatically created by Docker)

    3:  NAMED VOLUMES 
         docker run -v  name:/var/lib/mysql/data
                    /var/lib/docker/volumes/random-hash/_data
                name: Is up to me ,
        You can reference the volume by name 

        NB: NAMED VOLUMES is recommended . Should be used in production 

## DOCKER VOLUME LOCATIONS
    window c:\ProgramData\docker\volumes
    Linux   /var/lib/docker/volumes
    Mac     /var/lib/docker/volumes

    Each volume has unique hash cfc1ab....ddf22/_data
    Docker for Mac creates a Linux virtual machine annd stores all the Docker data here .
    $ screen ~/Library/Containers/com.docker.docker/Data/com.docker.driver.amd64-linux/tty
        physical storage of my app
    / # ls
    / # ls /var/lib/docker
            containers
            network
            plugins
            tmp
            volumes
            images
            overlay2
            swarm
            trust

    / # ls /var/lib/docker/volumes
    / # ls /var/lib/docker/volumes/hhhhhhhhhhhh_mongo-data/
    / # ls /var/lib/docker/volumes/hhhhhhhhhhhh_mongo-data/_data
    / # ctrl + a + k
     $ screen ls

## INSIDE THE CONTAINER
    $ docker exec -it     53eb5c04be0b sh
    $ ls /data/db
    