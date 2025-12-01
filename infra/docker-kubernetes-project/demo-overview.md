## DEMO PROJECT OVERVIEW
    Workflow with Docker
      - Deployment  
      - Continuous Integration /Delivery
      - Deployment
    How docker integrate to above steps

## Workflow with Docker
    - Laptop(developing Javascript App use Mango DB(docker hub) ) - You start Developing
        Let say u develop the application locally ,deploy to the development ,tester can test
            Developing a Js App ====> commit ====> Git ======>Jenkins(CI) ====>Build JS App & Creates Docker Image =====>Push =======> Docker Resipostory(private repos)
                    =======> Pull (image from PR) ======>Dev Server pulls both images
                    They talk / communicate each other .
                    Devops will login into pr to test the application .

## Developing with Containers
        docker pull mongo
        docker pull mongo-express
        docker  images
      
        How to connect to containers ?  
            Host
                isolated network when conttainer running in

## DOCKER NETWORK
    - docker create its isolated network when the container is running
    - if I deploy two containers in the same network, they can communicate with each other
          # MongoDB
          # MONGO EXPRESS UI
          # Nodes Js (Front end)
    - They can talk to each other by using container name without localhost /port
    - They are on the same network
            Nodes Js (Front end) ====> MongoDB =====> MONGO EXPRESS UI

## DOCKER NETWORK 
    - To view the networks
        docker network ls
        docker network create mongo-network
        docker network ls
        Check the env in hub.docker.com/ mongo

## create docker network
         docker network create mongo-network
## start mongodb
        docker run -d \ 
            -p 27017:27017 \
            -e MONGO_INITDB_ROOT_USERNAME=admin \
            -e MONGO_INITDB_ROOT_PASSWORD=password  \
            --name mongodb \
            --net mongo-network \
            mongo
        docker logs  id

## start mongo-express
    Mongo-express   
        docker run -d \ 
            -p 8081:8081 \
            -e ME_CONFIG_MONGODB_ADMINUSERNAME=admin \
            -e ME_CONFIG_MONGODB_ADMINPASSWORD=password  \
            -e ME_CONFIG_MONGODB_SERVER=mongodb \
            --net mongo-network \
            --name mongo-express \
            mongo-express 

       will connect to mango db conntaioner
       docker ps
       docker  logs id | tail last activities
       docker  logs id -f 



# DockerFile
    Is the bluepring for building images
## DOCKER REGISTRY 
    Docker private repository
        - Amazon ECR
        - Create an account with AWS
        - Search for ECR- elastic container registry
        - Select the region
        - Create a repository
        - Add the name of respository : my-app
        - Click Create repository button
    Registry options

    If you want to push your image from host to registry
        - Docker login  check on aws
            Pre-Requisite
                - AWS CLI needs to be installed
                - Credentials configured

        - Docker build
        - Docker push