# Kubernetes Overview


**Kubernetes** 
- Open source container orchestration tool (manages multiples containers)
- Developed by Google
- Helps you  manage containerized applications in different deployment environments
    - physical
    - cloud
    - virtual

**Kubernetes Impact** 
- **Withour K8s**
    - Trend from monolith to microservices
    - Increased usage of containers
- **With K8s**
    - High Availability/ Zero downtime
    - Scalability/ High performance
    - Disaster recovery - Backup and restore
    - Hardware resouce management for each pods

#### Kubernetes Architecture

- **Master Node:**
  - Loosing masternode is loosing access to cluster
  - Requires less resource
  - Its Ideal to have 1 backup of master node running
  - Companies preffer having more than 2 master nodes running
  <details><summary>Kube-apiserver</summary>

   - Its a container
   - Only Entrypoint to K8s Cluster communication
   - Client like UI, API, CLI use it
  </details> 
  <details><summary>Kube-controller-manager (API)</summary>

  - Keeps track of health of cluster
  </details>
  <details><summary>Scheduler</summary>

  - Ensures Pods placement
  - Creation of Pods inside of nodes based on workload
  - Backup and Restore on disaster recovery are made from etcd snapshots
  </details>
  <details><summary>Etcd</summary>

  - Backing store
  - Key-Value pair Db
  - Stores all the meta data, status data of each node and container
  </details>

- **Virtual Network**
  - It glues all the Nodes inside the cluster into one powerful machine
  - Creates one unified machine

- **Worker Node:**
  - Dependent on Master Node
  - Requires higher resource
  <details><summary>Services (kubelet, kube-proxy)</summary></details>
  <details><summary>Pods</summary>
  
   - Smallest unit 
   - Abstraction/Wrapper over container(s)
   - Idea 1:1 for a pod:container, but pod can contain sub helper container required by the running container
   - Each pod is assigned New Internal IP (not the container) by Virtual Network on creation/re-creation
   - **Services**
        - Permanent IP (To manage dynamic ip)
        - Load balancer
        - Types:
        1) External Service:
            - Opens Communition from external sources
            - IP Range: 30000 – 32767
            - To have a secure protocol for access rather the ip:port, Ingress is used.
        2) Internal Service
  </details>

Kubernetes accesses images from DockerHub, AWS ECR, GitLab registry, and other sources.

### Kubernetes Configuration
All the configuration in K8s cluster goes through a master node(API Server), And request is made in YAML or JSON format

### ConfigMap & Secret
We can use this Variables/definitions in app or service file using env variable or property file
> ConfigMap:\
    - Excternal configurations of deploy app.\
    - Example: Urls, dir path, etc.

> Secret:\
    - To store Credentials, certificates, etc.\
    - Similar to config map, used to store secret data\
    - Stored in base64 encode

### Volumes
- Attaches physical storage to the pod
- Attached storage can be local/ remote
- Use to avoid data loss when pod fails
- Data is not managed by K8s and its owners risk

## Deployment & Stateful Set
In practice we use deployments rather pods/replica files
> Deployment:\
    - A blueprint to manage Pods and ReplicaSets for scaling and updates. \
    While Service provides networking and load balancing for Pods and is not managed by Deployments\
    - Abstraction of Pods\

For Pods to which Volume is attached, Deployment cant be use.
Assume DB file used by many POD replicas will endup inconsistant, To fix this issue Stateful Set is used.
> Stateful Set:\
    - To store Credentials, certificates, etc.\
    - Similar to config map, used to store secret data\
    - Stored in base64 encode