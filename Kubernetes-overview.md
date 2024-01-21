Pre-learning: https://www.youtube.com/watch?v=wXuSqFJVNQA&ab_channel=TravisMedia

# Kubernetes Overview

Kubernetes or k8s

### Containers: 
 - Docker is most famous
 - Software requires different prerequisite depends on software version, platform, architecture etc
 - to overcoome this issue, each required softwares are packed as container. with this chagne, each software's prerequisite has been met inside the container, no need to change library or dependencies for each of the software

### Containers vs Virtual Machines
![Screenshot 2024-01-21 at 4 06 43 PM](https://github.com/JacobJae/studyKube/assets/38265255/5d503d37-7ee3-4427-94d0-ca996b6fbdb6)

Key difference is that Hypervisor create another OS for each VM while Docker shares same OS for all Container
It makes Docker to reduce utilization cost, less space and faster on boot.
However, Windows container can not run on linux docker
Both Docker and Hypervisor are not compatible with different kernel architectures. i.e. linuxamd hypervisor cant create ppcle VM and linuxamd container can not run on ppcle docker

How is it done?
By running `docker run ansible`, you can start ansible instance. You can also start multiple instances by configuring load balancer 

### Process vs Instance
Process refers specifically to an executing instance of a program with its own resources and state in the context of an operating system.
Instance is a more general term that can refer to a particular occurrence or realization of something, which could include software applications, services, or components.

### Container vs Image
Image: Package Template Plan(i think its kinda like a recipe), use image to create container.
You can create a Docker image on one operating system and run it on another, as long as both systems are running Docker (Architecture dependent, can't run linuxamd image on ppcle)

### Container orchestration
Container orchestration is the automated management, deployment, scaling, and operation of containerized applications
Popular container orchestration platforms include Kubernetes, Docker Swarm, and Apache Mesos.

### Kubernetes architecture
Node: (previously called minion)
- physical or virtual machine that installed Kubernetes
- node is a worker machine that kuberbetes will launch containers

Cluster: consists of multiple nodes
- provide HA
- multiple nodes help sharing load
- master node and worker node

### Kubernetes compenents
- API server
  - Front-end for kube, interact kubernetes
- etcd service
  - distributed reliable key-value store used by kubernetes to store all data used to manage the cluster
  - make sure there is no conflict on masters (i think it means prevent split brain)
- kubelet service
  - agent that runs on each node of cluster
  - agent is responsible for containers are running on node as epexted
- Container runtime
  - responsible for running application in containers
  - underlying software used to run the container (eg, Docker, rkt, CRI-O)
- Controller
  - monitor node goes down, if it goes down, controller bring up new container
- Scheduler
  - distributing work or containers across multiple nodes
 
### Master vs Worker nodes
<img width="955" alt="Screenshot 2024-01-21 at 5 00 17 PM" src="https://github.com/JacobJae/studyKube/assets/38265255/95f00af0-1b34-4152-b0be-7a3aceb566df">

### kubectl
- main command to run kubernetes
- `kubectl run hello-minikube`
- `kubectl cluster-info`
- `kubectl get nodes`
