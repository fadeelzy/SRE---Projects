## UNDERSTANDING STORAGE OPTIONS
    Container may go down , this mean that the entire file will unvailable.The storage comes to solve the problem.
    
    Module Overview
    1. Storage Core Concepts
    2. Volumes
    3. Persistent Volume and Persistent Volume Claims
    4. Storage Class

# Storage Core Concepts
    Question:
        How do you store application state/data and excjange it between Pods with Kubernetes?
    Answer: Volumes (Although other data storage options are available)

    A Volume can be used to hold data and state for Pods and Containers.
    
    Pod State and Data
        Pods live and die so their file system is not persistent.
        Volumes can uses to store state/data and use it in a Pod .
        A Pod can hve multiple Volumes attached to it
        Containers rely on a mountPath to access a Volume .
        Kubernetes Supports :
            - Volumes
            - Persistent Volume
            - Persistent Volume Claims
            - Storage Class
# Volumes
    Pod  ======> Volume
    Container
    
     Volumes and Volume Mounts
        A volumes references a storage location
        Must have unique name
        Attached to a Pod and May or may not be tied tp the pods lifetimes(depend on volumes)
        Volumes mount refence a volume by name and defines a mountPath.
    
    Volumes Types Examples
        emptyDir : empty directory for storing "transient" data (shares a Pod lifetimes}
                    useful for sharing files between containers running in a Pod .

        hostPath : Pod mounts into the node's filesystem 
        nfs : An NFS share mounted into the Pod.
        configMap/Secret : Special types of volumes that provide a Pod with access to Kubernetes resources.
        persistentVolumeClaim : Provides Pods with a more persistent storage. option that is
                abstracted from the details .
        cloud : Cluster wide storage 

    We have alot of options for volumes.  Find the examples  of the code in the lists
# Cloud Volumes
    Cloud providers (Azure , AWS , GCP ,etc) 
    Support different types of Volumes
        Azure - Azure Disk and Azure File
        AWS  - Elastic Block Store
        GCP - GCE Persistent Disk
    Example code of Azure File volumes see the code

# Viewing a Pod's Volumes
    Several different techniques can be used to view a Pod's Volumes.
        1: Describe Pod
            kubectl describe pod <pod-name>

        2: Get Pod YAML
            kubectl get pod <pod-name> -o yaml

# Volumes In Action
        See the examples of the code in Yaml file
            ngnix-alpine-emptyDir.pod.yaml 
            docker-hostPath.pod.yaml 

      Valid Types Includes:
        DirectoryOrCreate
        Directory
        FileOrCreate
        File
        BlockDevice
        charDevice
        

# Persistent Volume and Persistent Volume Claims
    A persistent volume is a cluster-wide storage unit provisioned by an administrator with a lifecycle
        independent from a Pod
             PV =====> Storage
              
    A persistent volume claim is a  cluster-wide storage resource that relies on network-attached storage
    Nomally provisioned by a cluster administrator.
    Available to a Pod even if it gets reschudeled to a different node.
    Rely on a storage provide such as NFS, cloud  etc
    Associated with a Pod by Using a Persistent Volume Claim(PVC)


    PersistentVolumeClaim is a request for a storage unit
        PVC =====> PV =====> storage
        
  
# PersistentVolume and PersistentVolumeClaim Yaml
    Pod ------> PVC --------> PV -------> Storage  
        Example on the Code 
        https://github.com/kubernetes/examples
             persistentVolumeClaim-azure.yaml
             persistentVolume-azure.yaml

# StorageClasses
    A StorageClass is a type of storage template that can be used to dynamically provision storage .
    Adminstrator will setup 
    StorageClasses are used to define different "classes" of storage
    Act as a type of storage template
    Support dyamic provisioning of PersistentVolumes

# SUMMARY
    Kubernets Supports several different types of storage
        - Emphemeral Volumes  (emptyDir)
        - Persistent Storage (Many options)
        - PersistentVolume 
        - PersistentVolumeClaims
        - Storage Classes
        - ConfigMaps (Key/value pairs)
        - Secrets (Key/value pairs)

### Creating ConfigMaps and Secrets 
    Module Overview
    ConfigMaps Core Concepts
    Using  a ConfigMap
    Secrets Core Concepts
    Creating a Secret
    Using a Secret

# ConfigMaps Core Concepts
        Provide a way to store configuration data that can be accessed by pods or 
        Provide a way to stpre configuration information and provide it to containers via cluster.

    ConfigMaps 
        Pods       ========>  ConfigMaps    
        Containers
    Provides a way to inject configuration data into a container
    Can store entire files or provide key / value pairs
        - Store in file . Key is the filename , value is the file contents
            (can be JSON , XML , Keys/Values) .
        - Provide on the commandline
        - ConfigMap

 # Accessing ConfigMaps Data in Pod
    ConfigMaps can be accessed from a Pod using:
        - Environment Variables (key/value pairs)
        - ConfigMap volume(access as files)

# ConfigMaps Core Concepts 
    See the exmple of the code in the Yaml file
        configmap-env.yaml
    Creatig a ConfigMap
    A ConfigMap can be created using kubetcl create
    Key command line switches includes
            --from-file
            --from-literal
            --from-env-file

 # Creating a ConfigMap using from config file
    kubetcl create configmap <configmap-name> --from-file=<path-to-file>

 # Creating a ConfigMap using from env file
    kubetcl create configmap <configmap-name> --from-env-file=<path-to-file>

 # Create a ConfigMap  from individual key/value pairs
    kubetcl create configmap [cm-name]
        --from-literal=apiUrl>=https://api.example.com
        --from-literal=otherKey=otherValue

# Create from a ConfigMap manifest
    kubetcl create -f file.configmap.yaml
 
## Using a ConfigMap
    Getting a ConfigMap
     kubetcl get configmap can be used to get a ConfigMap and view its contents .

  # Get a ConfigMap
    kubetcl get configmap [cm-name] -o yaml

  # Accessing a Config :Volume
    ConfigMap values can loaded  through a volume .
    Each key is converted to a file - value is added into the file  
  
# ConfigMMap in Action     
# Secrets Core Concepts
    A secret is an object that contains a small amount of sensitive data such as 
    password, a token , or a key.
  
    Secrets 
        Kubernetes can store sensitive information in a secret.(password, keys and certificates)
        Avoids storing secrets in container images , in files , or in development environments.
        Mount secrets into pods as files or as environment variables.
        Kubernets only makes secrets available to Nodes that have a Pod requesting access to it.
        Secrets are stored in tmpfs on a Node (not on disk)
          https://kubernetes.io/docs/concepts/configuration/secret/#best-practices
 
    Secrets Best Practices
         Enable encryption at rest for cluster data 
            https://kubernetes.io/docs/tasks/administer-cluster/encrypt-data/
         Limit access to etcd (where secrets are stored)
            https://kubernetes.io/docs/tasks/administer-cluster/limit-etcd-access/
         Use SSL/TLS for etcd peer-to-peer communication
         Manifest(YAML/JSON) file only base64 encoded the secret
         Pods can access Secrets so secure which users can create Pods. Role-based access control
            (RBAC) can be used to restrict access to Secrets.

# Creating a Secret
    Secret can be created using kubetcl create secret

 # Create a secret and store securely in kubernetes
    kubetcl create secret generic my-secret 
        --from-literal=pwd=my-password
# Create a secret from a file
    kubetcl create secret generic my-secret 
        --from-file=ssh-privateKey=~/.ssh/id_rsa
        --from-file=ssh-publicKey=~/.ssh/id_rsa.pub
# Create a secret from a key pair
    kubetcl create secret tls tls-secret --cert=path/to/tls.cert --key=path/to/tls.key

    example of the yaml file
        secret.yaml

  # Using a Secrets 
        Listing Secret Keys
            A List of secret can be retrieved using kubetcl get secret
            # Get a Secret
                kubetcl get secret 
            # Get YAML for specific secret
                kubetcl get secret db-secret -o yaml

## SUMMARY 
    ConfiMaps provide a way tpo stpre configuration data
    Secrets provide a way to store sensitive data or files
    Secrets are stored in tmpfs on a Node (not on disk)
    Access key/value pairs usings Environment Variables  or Volumes
    Use caution when working with secrets and ensure proper security is in place .