### KUBERNETES INTRODUCTION
    - Moving to another environment
    - Gonna move from docker compose  file into kubernetes

### COURSE OVERVIEW
    Kubernetes from a Developer perspective
    Creating Pods
    Creating Deployments
    Creating Services
    Understanding Storage Options
    Creating ConfigMaps  and Secrets

# MODULE AGENDA
    - Beyond Docker Compose
    - Introduction to Kubernetes
    - Converting from Docker Compose to Kubernetes
    - Running Container in Kubernetes
    - Stoppping and Removing Containers in Kubernetes

# Beyond Docker Compose
    - How do you manage all of these containes in test/stage/production?
    - How are you Deploying/Managing your containers?
    - How Do You Scale and Load Balancer Vms?
    - It would Be Nice if You could
            * Package up an app , provide a manifest and let something else manage it for us
            * Not worry about management of containers
            * Eliminate single points of failures and self-heal containers
            * Have a robust way to scale and load balance containers
            * Update containers without bringing down the whole app
            * Have a robust networking and persistent storage options

    - Docker compose isnt intended to used a production environment, across to a different environment.
    - What if we could define the containers we want and then hand it off to a system that manages it all for us?
            ## WELCOME TO KUBERNETES 

### INTRODUCTION TO KUBERNETES
    * https://kubernetes.io/docs/concepts/overview/
    - Is an open-source system for automating deployment ,scalling, and management of containerized applications
    - Kuberenetes is the coach of a container team

# KUBERNETES OVERVIEW
    - Container and cluster management
    - Support by all major cloud providers 
    - Provides a declarative way to manage containers and clusters
    - Provides a declarative way to define a cluster's state using manifest files(YAML)
    - Interact with Kuberenetes  using kubectl

# KEY FEATURES
    - Service Discovery/Load Balancing
    - Storage Orchestration
    - Automate Rollouts/Rollbacks
    - Manage Workloads
    - Self-Healing
    - Secret and Config Management
    - Horizontal Scalling
    - More , networing

# KUBERNETES - THE BIG PICTURE
    - Have a MASTER - In charge of all the children
    - Child  - Node (Pod) Node (Pod) Node (Pod) ,you can put mmultiple thing in the POD, Can run in multiple nodes
    - Multile node  which are managed by the master we call CLUSTER

## RUNNING KUBERNETES LOCALLY
    -Minikube
        https://github.comm/kubernetes/minikube
    - Docker Desktop
        https://www.docker.com/products/docker-desktop
    - Enabling Kuberenetes on Mac
        https://kubernetes.io/docs/setup/production-environment/tools/kubeadm/enabling-kubelet-on-MAC/

# KEY KUBERNETES CONCEPTS
    - Deployment 
        * Describes desired state (yaml Json)
        * Can be used top replicate pods
        * Support rolling updates and rollbacks

    - Service   
        * will be incharge of exposing the pods
        * Pods live and die
        * Services abstract the pod IP addressess from consumers
        * Load balances between pods
            service 10.0.0.1
                    pod [container] 10.0.0.43
                    pod [container] 10.0.0.53

## CONVERTING FROM DOCKER COMPOSE TO KUBERNETES
    - Migrating from Docker Compose file to Kubernetes
        - Compose on Kubernetes 
            https://github.com/docker/compose-on-kubernetes
            docker stack deploy --orchestrator=kubernetes -c docker-compose.yml test
        - Kompose
            https://kompose.io

## RUNNING CONTAINERS IN KUBERNETES
    - Run the containers in kubernates
    - Key Commands
        kubectl version
        kubectl get [deployments| services|pods]
        kubectl get deployments
        kubectl get deploy
        kubectl get services
        kubectl get pods
        kubectl run nginx-server --image=nginx:alpine
        kubectl run nginx-server --image=nginx:alpine
        kubectl apply -f [fileName | folderName]
        kubectl apply -f ./.k5s
        kubectl port-forward [name-of-pod] 8080:80
        kubectl delete deployment nginx-server

## STOPPING AND REMOVING CONTAINERS IN KUBERNETES
    -KEY COMMANDS
        - kubectl delete [FILENAME|FOLDER]
        - kubectl delete [deployment|service|pod] [name-of-pod]
        - kubectl delete [deployment|service|pod] [name-of-pod] --grace-period=0
        - kubectl delete [deployment|service|pod] [name-of-pod] --force
        - kubectl delete [deployment|service|pod] [name-of-pod] --grace-period=0 --force
        - kubectl delete -F ./k5s

### SUMMARY
    - Kubernetes is a container orchestrated system
    - Kubernetes provides a robust solutions for automating deployment, scaling, and management of containerized applications
    - Provides a way to move to a desired state.
    - Relies on YAML (or JSON) files to represent desired state
    - Nodes (VM) and Pods(act group container play a central role in Kubernetes   
    - A container runs in a pod
    - Kubectl can be used to issue commands and interact with the kubernetes API
