### DOCKER REGISTRY  OVERVIEW
    - Docker private repository
    - Registry options
    - Amazon ECR
    - Build and Tag Image
    - Pushing our build docker image into private Registry on AWS
    - docker login
    - docker push

## CREATE PRIVATE REPOSITORY DOCKER REGISTRY ON AWS
    - aws 
        ECR
            Create repository
                Repository name  : my-app
                    Create repository
            each image

## PUSH THE IMAGE FROM LOCALLY INTO PR
    - You always have to login to private repo  = docker login
        docker login
        $(aws ecr get-login --no-include-email --region eu-central-1)
            Pre-Requisites
                1: AWS CLI needs to be installed
                1: Credentials configured
 
## IMAGE NAMING INN DOCKER REGISTRIES
     registryDomain/imageName:tag
        - In DorkerHub
            $  docker pull mongo:4.2
            $  docker pull docker.io/library/mongo:4.2
            

     In AWS ECR :
         $ docker pull aws_account_id.dkr.ecr.us-west-2.amazonaws.com/amazonlinux:latest
 
## PUSHING OUR DOCKER IMAGE INTO A PRIVATE REGISTRY ON AWS
          $ docker tag my-app:1.0  aws_account_id.dkr.ecr.us-west-2.amazonaws.com/my-app:1.0
          $ docker ps
          $ docker push s_account_id.dkr.ecr.us-west-2.amazonaws.com/my-app:1.0
            push the image layer by layer , once the push has completed ,you can see the image aws
                docker tag =  rename the image 

## MAKE SOME CHANGES TO THE APP, REBUILD AND PUSH A NEW VERSION TO AWS REPO
        $ docker build -t my-app:1.1 .
        $ docker images
        $ docker tag my-app:1.1 ws_account_id.dkr.ecr.us-west-2.amazonaws.com/my-app:1.1 
        $ docker images
        $ docker push my-app:1.1 ws_account_id.dkr.ecr.us-west-2.amazonaws.com/my-app:1.1 

       NB: Docker login always in, my-app in aws can have tone of image on the same name
            Jenkins also needs tto login to your private repo
         