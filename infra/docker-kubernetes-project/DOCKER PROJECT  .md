## DEMO PROJECT OVERVIEW
    Workflow with Docker
      - Deployment  
      - Continuous Integration /Delivery
      - Development
      
## Workflow with Docker
    - Laptop(developing Javascript App) ====commit====>Git======>Jenkins(CI)====push=====>Docker Resipostory

## DOCKER NETWORK
    - docker create its isolated network when the container is running
    - if I deploy two containers in the same network, they can communicate with each other
          # MongoDB
          # MONGO EXPRESS UI
    - They can talk to each other by using container name without localhost /port
    - They are on the same network

## DOCKER NETWORK 
    - To view the networks
        docker network ls
        docker network create mongo-network

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