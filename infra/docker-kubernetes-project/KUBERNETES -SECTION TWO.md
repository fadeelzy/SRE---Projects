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

### MODULE OVERVIEW
    Kubernetes Overview
    The Big Picture
    Benefits and Use Cases
    Running Kubernetes Locally  
    Getting Started with Kubectl
    Web UI Dashboard

## Kubernetes Overview
    "k8s is an open source system for automating deployment, scaling, and management
        of containerized applications."
          https://kubernetes.io

## Managing the Container
    Server  ===> API ===> Redis
                 API 
                 API ===> db
    How do you manage all of these containes in test/stage/production?
    - How do you manage all of these containes in test/stage/production?
    - How are you Deploying/Managing your containers?
    - How Do You Scale and Load Balancer Vms?
    - It would Be Nice if You could
            * Package up an app , provide a manifest and let something else manage it for us
            * Not worry about management of containers
            * Eliminate single points of failures and self-heal containers
            * Have a robust way to scale and load balance containers
            * Update containers without bringing down the whole app
            * Have a robust networking and persistent storage options ,container can talk to each other.
            * Example :Take Ochestor  .The Kubernetes (conductor) - Inside the venue you will many
            containers, if once container is failed , The job of conductor is to bring it back up.
     NB:Kubernetes is the conductor -> orchestra container.

    - Docker compose isnt intended to used a production environment, across to a different environment.
    - What if we could define the containers we want and then hand it off to a system that manages it all for us?
            ## WELCOME TO KUBERNETES 
# KEY FEATURES
    - Service Discovery/Load Balancing-kubernetes.The grp of machine that working together to run our containers.
    - Storage Orchestration - As Volume
    - Automate Rollouts/Rollbacks - Deployment , we can archive by zero time deployment
    - Manage Workloads -
    - Self-Healing - Bring up container if goes down
    - Secret and Config Management
    - Horizontal Scalling - Scale up and down(memory)
    - More , networking

## The Big Picture
    - Have a MASTER - In charge of all the children
    - MASTER - This is boss 
    - worker node :Server / physical machine
    - Child  - Node (Pod) Node (Pod) Node (Pod) ,you can put mmultiple thing in the POD, Can run in multiple nodes
    - Multile node  which are managed by the master we call CLUSTER
    - Pod host the containers
    - Container and cluster management
    - OS project
    - Cloud support
    CURRENT STATE    ===> K8S ========> DESIRED STATE
    Container                           container container container    

## PODS AND CONTAINERS
    - Pod is like a box which container goes in                      
    - We can have multiple pods on Kubernetes                    
    
## Kubernetes build blocks
    Master
       Store(etcd)
       API (Yaml, JSON)
       Controller Manager
       Scheduler
    Will manage all the nodes
    Developers can use $kubectl to manage the pods
    You need the way the pods to communicate with each other
        Deployment  ==>Pod (Container)  , Pod (Container)  , Pod (Container)  
        Replicaset  ==>Pod (Container)  , Pod (Container)  , Pod (Container) 
    The communication is done by kubernetes services
    we can send Yaml/Json  to the server and it will create the pod 

## KUBERNETES NODES
    Each  nodes has additions of pods running ,we need the mechanism to communicate back
    and forward to the Master
    Based on that , we shoud install the plugin called kubelet ,to allwo to communicate with Master.
    kubelet is a plugin which is installed on all the nodes
    We need the Container runtime to run with the pod
    We need the netwoking plugin to run with the pod- kube-Proxy
    The kube-proxy makes the pods gets the unique address

### Benefits and Use Cases
      I am a developer ,why do I need to install kubernetes?
      Accelarate development as developer
      Eliminate conflicts    
      Enviroment  Consistency dev, Prod 
      Ship software Faster

### Key Kubernetes Benefits
      Orchestrate our containers
      Zero downtime deployment
      Self-healing   (superpowers) 
      Scale our containers horizontally

### Key Container Benefits
    Accelerate developer Onboarding
    Eliminate App conflicts
    Enviroment Consistency
    Ship Software Faster
 
    NOTE: The above is great but what if  the company has  decided to move to the next level ?

### Developer Use Cases and Benefits  
    Emulate production environment locally
    Move from Docker Compose to Kubernetes
    Create an end to end  test environment
    Ensure application scales properly
    Ensure security/ config properly
    Performance testing scenarios
    Workload scenarios (CI/CD)
    Learn how to leverage  deployment
    Help DevOps create resource and solvee problems

### RUNNING KUBERNETES LOCALLY
    # Installing and Running Kubernetes
        Minikube            https://github.com/kubernetes/minikube
        Docker Desktop      https://www.docker.com/products/docker-desktop 
        Kind                https://kind.sigs.k8s.io
        Kubeadm             https://kubernetes.io/docs/reference/setup-tools/kubeadm/kubeadm

        kubetcl get all

### GETTING STARTED WITH KUBECTL
    Getting Started with Kubectl Commands
        Check kubernetes version
            kubectl version
        View cluster information
            kubectl cluster-info

        Retrieve information about kubernetes Pods, Deployments, Services, and Nodes
            kubetctl get all

        Retrieve a Specific Service
            kubectl get pods
            kubectl get deployments
            kubectl get services
            kubectl get nodes 

        Simple way to create a Deployment for a Pod
            kubectl run [container-name] --image=[image-name]
            kubectl run [container-name] --image=[image-name] --port=[port-number]

        Forward a port to allow external eccess
            kubectl port-forward [pod] [port]

        Exposee a port for a Deployment/Pod 
            kubectl expose ...  

        Create a resource
            kubectl create [resource]

        Create  or modify a resource
            kubectl apply [resource]

## Aliasing kubectl (to save on typing)
 # PowerShell
    Create alias for PowerShell
        set-Alias --Name k -Value kubectl

# Mac/Linux
    Create alias for Mac/Linux  Shell
        alias k="kubectl"

### Web UI Dashboard
    Web UI Dashboard provides a user interface to view kubernetes resources
        https://kubernetes.io/docs/tasks/access-application-cluster/web-ui-dashboard/
    Steps to enable the UI Dashboard:
         kubetctl apply [dashboard-yaml-url]
         kubetctl describe secret -n kube-system 
         Locate the kuberntes.io/service-account-token and copy the token
         kubectl proxy  
         visit the dashboard URL and login using the token

### Summary
    Kubernetes provides container orchestration capabilities
    Use for productions , emulating production, testing and more
    Several options are available to run kubernetes locally
    Interact with Kubernetes using kubectl

### CREATING PODS
    Module Overview
        Pod Core Concepts
        Creating a Pod  
        kubetcl and Pods
        YAML Fundamentals
        Defining a Pod with YAML
        Pod Health (developer)

 # Pod Core Concepts
    A pod is the basic execution unit of a Kubernetes application-the smallest
    and simplest unit in the Kubernetes object model that you create or deploy.
    Think as Building Block
    Kubernetes pods runs the containers
    Smallest object of the Kubernetes object model
    Environment for containers   
    Organize application "parts" into Pods (Server ,caching ,API ,Database) 
    Pod has the IP , memory , Volumes, etc shared across containers
    Scale horizonally by adding Pod replicas
    Pod live and die but never come back to life

## The Role of Pods
    Pod containers share the same Network namespace (share IP / Port )
    Pod containers have the same loopback interface (share IP / Port )
    Container processes need to bind to different ports within a Pod
    Ports can be resused by containers in separate Pods
   
# Nodes and Pods
    Pods do not span nodes

## Creating a Pod
    Running a Pod
       There are several different ways to schedule a Pod:
            kubetctl run command
            kubetctl create/apply command with a yaml file

   # Run the nginx:alpine container in a Pod
        kubetcl  run [pod-name] --image=nginx:alpine
   # List Only Pods
        kubetcl get pods
   # List all resources
        kubetcl get all

##Get Information about a Pod
    The kubectl get command can be used to retrieve information about Pods and Many
      other Kuberneted objects

## Expose a Pod Port
    Pods and containers are only accessible within the Kubernets cluster by default
    One way to expose a container port externally:
        kubectl port-forward

 # Enable Pod container to be called externally
    kubectl port-forward  [port-number] 8080:80   External Port:Internal Port

# Will cause pod to be recreated
    kubectl delete pod [name-of-pod]
# Delete Deployment that manages the Pod
    kubectl delete deployment [name-of-deployment]

    Deleting a Pod
      Running a Pod will cause a Deployment to be created
      To delete a Pod use kubectl delete pod or find the deployment and use kubectl delete deployment

 # kubetcl and Pods
    kubectl get all
    kubectl run ngnix --image=nginx:alpine
    kubectl get pods
    kubectl get services  
     note: CLUSTER-IP is internal address of the pod
    kubectl port-forward ngnix 8080:80 
    kubectl get pods
    kubectl delete  pod ngnix
    kubectl get pod

    Working with Pods Using kubetcl
    Different kubectl commands can be used to run , view , and deleted Pods
     Summarry
       kubectl run [pod-name] --image=nginx:alpine
       kubectl get pods
       kubectl  forward pod [pod-name] 8080:80
       kubectl  delete pod [pod-name]
    "If your 1.18+ "run" only creates the Pod but < 1.18 + "run" creates the Pod and other resources"

 # YAML Fundamentals
    is the text files
    Yaml files are composed of maps and lists
    Indentation matters 
    Always use spaces
    
    Maps:
        - name:value pairs
        - Maps can contain other maps for more complex data structures

    Lists:
        - Sequences of Items
        - Multiple maps can be defined in a list

      key: value
      complexMap:
        key1: value
        key1:
           subkey: value
      items:
        - item1
        - item2
        - item3
      itemsMap:
        - map1: value
          map1Pro: value
        - map2: value1
          map1Pro: value
    Yaml maps define a key and value 
    More complicated map structures can be defined using a key that references another map
    Yaml lists can be used to defined a sequence of items   
    Yaml lists can be used to defined a sequence of Maps 

    # NB: Indentation matters , use spaces not tabs
    
 # Defining a Pod with YAML
    Yaml (Pod) + kubectl  =   Pod  and containers

apiVersion: v1        # kubectl API version
kind: Pod             # Type of kubernetes resource
metadata :            # Metadata about the Pos
name: my-nginx
spec:                 # The spec / blueprint of the Pod
containers:         # Information about the containers that will run in the Pod
- name: my-nginx
image: nginx:alpine

## Creating a Pod Using YAML
    To create a pod using YAML use the kubeectl create command along with  --filename or -f switch

# Perform a "trial" create and also validate the YAML
    kubectl create -f file.pod.yml --dry-run  --validate=true
# Create a Pod from YAML    
# Will error if Pod  already  exists  
    kubectl create -f file.pod.yml

# Creating or Applying Changes to a Pod
    To create or apply changes to a pod using YAML use the kubectl apply command along with  --filename or -f switch

# Alternate way to create or apply changes to a Pod from YAML
    kubectl apply -f file.pod.yml   
# Use --save-config when you want to use kubectl apply in the future
    kubectl apply -f file.pod.yml --save-config 
        --save-config  : Store current properties in resource's annotations
        Causes the resource's configuration settings to be saved in the annotations.
        Example of saved configuration
        Having this allows in-place changes to be made to a Pod in the future using
            kubetc apply -f file.pod.yml
    kubectl delete -f file.pod.yml 
    kubectl delete pod [pod-name]
    
    NB: We can use the yaml file to create a  Pod

# Kubettl VS YAML

    We have seen that YAML is a text file that is used to define a Pod
    kubectl create -f nginx.pod.yml --save-config
    kubectl desctibe pod [pod-name]
    kubectl apply -f  nginx.pod.yml
    kubectl exec  [pod-name] -it sh
    kubectl edit    -f    nginx.pod-2.yml
    kubectl delete  -f  nginx.pod-2.yml

    Create and Inspect Pods with kubetcl
    Several different commands can be used to create and modify Pods

 # Pod Health (developer)
    Kubernetes relies on Probes to determine the health of a Pod container
    Probe is a diagnostic performed periodically by the kubelet on a container

 # Types of Probes
    Liveness Probe
        Can be used to determine if a Pod is healthy and running a expected
    Readiness Probe
        Can be used to determine if a Pod should receive traffic/ requests
    Failed Pod containers are recreated by default (RestartPolicy defaults to Always)
    How do we know if the pod is health or no? depend on software
        ExecAction -Executes an action inside the container
        TCPSocketAction -Sends a TCP request to a port on the container/Check against the containers IP address on a specified port
        HTTPGetAction -Sends an HTTP request to a specified URL / request against container's 
    Probes can have the following results:
        Success - The probe succeeded in its check
        Failure - The probe failed in its check
        Unknown - The probe is in an unknown state
    
    # Readiness Probe:
        When should a container start receiving traffic ?

    # Liveness Probe:
        When should a container start restart ? eg live or health issues

## POD HEALTH  IN ACTION
    - check in the ngnix.pod-3.yml file

## SUMMARY 
    Pods are the smallest unit of work in Kubernetes
    Containers run within Pods and sharea Pod's memory, IP ,Volumes and more
    Pods can be started using different  kubectl commands
    Pods can be used to create a Pod 
    Health checks provide a way to notify kubernetes when a Pod has a problem
    If the pods/ goes down or deleted for some reason , nothings will bring back to life


### CREATING DEPLOYMENTS
    If the pods/ goes down or deleted for some reason , nothings will bring back to life but deployment will bring back
    
    Module Overview
      Deployment Core Concepts
      Creating a Deployment
      Kubectl and Deployments
      Kubectl Deployments in Action
      Deployment Options
      Zero Downtime Deployments

 ## Deployment Core Concepts
    We will discuss in high level of the deployment
    A ReplicaSet is a declarative way to manage Pods   (Think as boss of Pod ,play behind the scenes)
    A Deployment is a declarative way to manage Pods using ReplicaSet under the cover   
  
 ## Pods , Deployments and  ReplicaSets
    Pods represent the most basic resource in Kubernetes
    Can be created and destroyed but are never recreated
    What happen if a Pod is destroyed ?
        - Deployments and ReplicaSets ensure Pods stay running and can be used to scale Pods

# The Role of ReplicaSets
    ReplicaSets act as a Pod Controller:
        Self-healing mechanism
        Ensure the requested number of Pods are available
        Provide fault-tolerance
        Can be used to scale Pods
        Relies on a Pod Template
        No need to create Pods directly
        Used by Deployments

# Result Of Creating a Replicaset
    kubectl get all

# The Role of Deployments
    Deployment :- high level WRAPPER
        ReplicaSets
            Pod
                Container

    A Deployment manages Pods:
        Pods are managed using ReplicaSets
        Scales ReplicaSets, which scale Pods
        Support zero-downtime updates by creating and destroying ReplicaSets
        Provides rollback functionality
        Creates a unique "label" that is assigned to the ReplicaSet and generated Pods
        Yaml is very similar to a ReplicaSet

 ## Creating a Deployment
    Defining a Deployment with YAML
    YAML (Deployment) + kubectl =   Deployment
                        ReplicaSet
                            Pod
                                Container
    Please check the example in the deployment-high-level-2.yml file

apiVersion: apps/v1        # kubectl API version and resource type (Deployment)
kind: Deployment
metadata :                # Metadata about Deployment
spec:
    selector:              # Select Pod template labels
        template:             # template used to create the Pods
            spec:
                containers:     # Containers that will run in the Pod
                        - name: my-nginx
                            image: nginx:alpine

 ## Kubectl and Deployments
    # Create a Deployment
        kubectl create -f file.deployment.yml
    # Creating or Applying Changes
        Use the kubectl apply command along with the --filename or -f switch

 # Creating  a Deployment with kubectl
    Use the kubectl create command along with the --filename or -f switch

# Alternative way to create or apply changes to a Deployment from YAML
    kubectl apply -f file.deployment.yml

# Use --save-config when you want top use kubetcl apply in the future
    kubectl create -f file.deployment.yml --save-config  

# Getting Deployments
    List all Deployments
        kubectl get deployments

# Deployments and Labels
    List the labels for all Deployment using the --show-labels switch
        kubectl get deployments --show-labels
    To get information about a Deployment with a specific label , use the - I switch
        kubectl get deployments  -I app=ngnix  

# Delete Deployment
    To delete a Deployment use kubectl delete 
    Delete Deployment and all associated Pods /Containers
        kubectl delete deployment [dep-name]

# Scale the Deployment Pods to 5
    Kubectl scale deployment [dep-name] --replicas=5  
    Scale Pods Horizontally
    Update the YAML file OR use kubectl scale command

# Scale by refencing the YAML file
    Kubectl scale -f file.deployment.yml --replicas=5  
    Scale Pods Horizontally
    Update the YAML file OR use kubectl scale command
        spec:
            replicas: 5
            selector:
                tier: frontend
                    
 ## Kubectl Deployments in Action
    - We have seen the command above ,let us put as real example.
    - Commands for Deployments
            kubectl create -f ngnix-deployment.yml --save-config
            kubectl describe [deployment | pod | [pod-name | deployment-name] 
            kubectl apply -f ngnix-deployment.yml
            kubectl get deployments --show-labels
            kubectl get deployments  -l app=my-nginx
            kubectl scale -f ngnix-deployment.yml --replicas=3
            kubectl delete deployment ngnix.deployment.yml

 ## Deployment Options
    How do you update Existing Pods?
        Current Pod
            Container
            ngnix:1.14.2-alpine  

                Change Image

        Desirable Pod
            Container
            ngnix:1.15.9-alpine     
                
     Zero downtime deployments allow software updates to be deployed to production without
     impacting end users /bring down the older version.
    One of the strength of Kuberneteds is Zero downtime deployments.
    Update an appplication's Pods without impacting end users.
    Several options are available :
        - Rolling Updates
        - Blue-green deployments
        - Canary deployments (small amount of traffic )
        - Rollbacks  (rollback to previous version)
        
 ## Rolling Deployments
    - Initial Pod State
        Pod (app-v1)
        Pod (app-v1)
        Pod (app-v1)
       
     Rollout New Pod
    Pod (app-v1)
    Pod (app-v1)
    Pod (app-v1)
            Pod (app-v2)
    One of older pod will be deleted
    sec of older pod will be deleted
            Pod (app-v2)  new pod will be created
            Pod (app-v2)  new pod will be created
            Pod (app-v2)  new pod will be created
 
 ##    Updating a Deployment
    Update a deployemnt by changing the YAML and applying changes to the cluster with kubectl apply
 # Apply changes made in YAML file
    kubectl apply -f file.deployment.yml

 ## Zero Downtime Deployments in Action

 ## Summary
    Pods are deployed , managed , and scaled using deployment and ReplicaSets.
    Deployments are a higher-level resource that define one or more Pod template
    The kubectl create or apply commands can be used to run a deployment.
    Kubernetes support xero downtime deployments.

### CREATING SERVICES
    - How pod can be accessed from outside the cluster/ get IP address
    Module Overview
        Services Cores Concepts
        Service Types
        Creating a Service with Kubectl
        Creating a Service with YAML

 # Services Cores Concepts
    A Service provides a single point of entry for accessing one or more Pods .

    Since Pod live and die , can you rely on their IP Address?
        Example 
            External Caller ======> Front-end Pod ======> Backend-end Pod
                                    Container             Container  
                                    10.0.0.43             10.0.0.45
        The answer is No , we  can't with Pod Id , we nned Services . IPs change  frequently.
        Services are a way to get the IP address of a Pod.
        
    The Life of a Pod
        Pod
        containers
        10.0.0.23
        - Pods are "Mortal" and may only live a short time.
        - You can't rely on a Pod IP address staying the same.
        - Pod can be horizontally scaled so each Pod gets its own IP address.
        - A Pod gets an IP address after it has beeen scheduled (No way a clients to know IP address in advance ).

    The Role of Service
        - Service abstracts the Pod IP address from consumers
        - Load balances between Pods
        - Relies on labels to assign Pods to Services
        - Node's kube-proxy creates a virtual IP for Services
        - Layer 4 (TCP/UDP over IP)
        - Services are not ephemeral
        -Behind the scenes, creates endpoints which sit between the Service and the Pod.

## SERVICES TYPES
    Service can be defined in different ways :
        ClusterIP
            Expose the servicce on a cluster internal IP (Default),This can talk to inetrnal IP address of their Pod.
            Service IP is exposed internally within the cluster.
            Only Pods within the cluster can talk top the Service
            Allows Pod to talk tp other Pods
        NodePort
            Expose the Service on each Node's IP at static port. 
            Expose the Service on each Node's IP at a static port.
            Each Node proxies the allocated Port.
        LoadBalancer
            Provision an external IP address to act as load balancer for the Service. 
            Exposes a Service externally .
            Useful when combined with a cloud provider's load balancer.
            NodePort and ClusterIP Services are created.
            Each Node proxies the allocated Port.

        ExternalName
            Maps a service to a DNS name
            Service that acts as an aliad for an external service
            External service details are hidden from cluster.(easier to manage)

## CREATING A SERVICE WITH KUBECTL
    Port Forwarding
        Qn : How can you access a Pod from outside of Kubernates ?
        Ans : Port Forwarding
    Use the kubectl port-forward command to access a Pod from outside of Kubernates.
    Use the kubectl port-forward to forward a local to a Pod port.

# Listen on port 8080 locally and forward to pod 80 in Pod
    kubectl port-forward pod/[pod-name] 8080:80

# Listen on port 8080 locally and forward to Deployment's Pod
    kubectl port-forward deployment/[deployment-name] 8080

# Listen on port 8080 locally and forward to Service's Pod
    kubectl port-forward service/[service-name] 8080

## CREATING A SERVICE WITH YAML
    Defining A Service with YAML
        YAML(Service) + Kubectl = service Pod Container

    Service Overview 
    Kubernetes API version and resource type (service
    See the example of all Services

## KUBECTL AND SERVICES
    Creating A Service
        Use the kubectl create command  along with the --filename or -f switch .
  # Create a Service
    kubetcl create -f file.service.yml

  # Update a Service
  # Assumes --save-config was used with create
    kubetcl apply -f file.service.yml

    Updating or Creating a Service
    Use the kubectl apply command along with the --filename or -f switch 

  # Deleting a Service
    Use the kubectl delete command along with the --filename or -f switch 
    kubectl delete -f file.service.yml

  # Testing a Service and Pod with Curl
    How can you quickly test if a Service and Pod is working ?
        Use kubectl exec to shell into a Pod/Container

  # Shell into a Pod and test a URL . Add -c [containerID]
  # in cases where multiple containers are running in the Pod
        kubectl exec [pod-name] -- curl -s http://podIP

  # Install and use curl (example shown is for Alpine Linux)
    kubectl exec [pod-name] -it sh
    >apk add curl
    >curl -s http://podIP

## KUBECTL SERVICES IN ACTION
    See all the example of service in yaml file

## SUMMARY
    Pods live and die so their IP addresses are reused.
    Services abstract Pod IP addresses from consumers .
    Labels associate a Service with a Pod . label used to organise the resources and gropu them
     Service Types :
        ClusterIP - Internal to service - default
        NodePort - exposes Service /Deployment on each's Node's IP
        LoadBalancer - exposes Service externally cloud / locally
        ExternalName - Service acts as an alias for an external service / proxy

















