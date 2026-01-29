# Kubernetes_N

# Monolithic vs. Microservices Architecture

Monolithic architecture is a traditional software development model where an entire application is built as a single, unified, and self-contained unit, with all components (UI, business logic, data access) tightly coupled in one codebase. It offers simplicity in development, testing, and deployment for small applications but becomes difficult to scale or maintain as complexity grows, often requiring full redeployment for any change. 

Benefits  - 

Simplicity in Development: Easier to develop, test, and deploy initially compared to microservices.

Performance: Generally faster, as components communicate directly within the same memory space rather than over a network.

Simplified Debugging: A single, centralized codebase makes it easier to trace requests. 

Microservices architecture is an approach to developing software as a collection of small, independent, and loosely coupled services, each implementing specific business functions. They communicate via APIs, allowing for independent deployment, scaling, and technology flexibility.

Benefits - 

Scalability: Individual components can be scaled independently based on demand.

Flexibility: Teams can use different programming languages or frameworks for different services.

Resilience: A failure in one service does not necessarily bring down the entire application. 

# Kuberentes? 
Kubernetes, is an open-source container orchestration platform designed to automate the deployment, scaling, and management of containerized applications.

# Kubernetes features - 
-- Service discovery and load balancing : Kubernetes can expose a container using a DNS name or their own IP address. If traffic to a container is high, Kubernetes is able to load balance and distribute the network traffic so that the deployment is stable.

-- Self-healing : Kubernetes restarts containers that fail, replaces containers, kills containers that don't respond to your user-defined health check, and doesn't advertise them to clients until they are ready to serve.

-- Horizontal scaling : Scale your application up and down with a simple command, with a UI, or automatically based on CPU usage.

-- Storage orchestration : Kubernetes allows you to automatically mount a storage system of your choice, such as local storage, public cloud providers, and more.

-- Automated rollouts and rollbacks : You can describe the desired state for your deployed containers using Kubernetes, and it can change the actual state to the desired state at a controlled rate. For example, you can automate Kubernetes to create new containers for your deployment, remove existing containers and adopt all their resources to the new container.

-- Automatic bin packing : You provide Kubernetes with a cluster of nodes that it can use to run containerized tasks. You tell Kubernetes how much CPU and memory (RAM) each container needs. Kubernetes can fit containers onto your nodes to make the best use of your resources.

-- Secret and configuration management : Kubernetes lets you store and manage sensitive information, such as passwords, OAuth tokens, and SSH keys. You can deploy and update secrets and application configuration without rebuilding your container images, and without exposing secrets in your stack configuration.

-- Batch execution : In addition to services, Kubernetes can manage your batch and CI workloads, replacing containers that fail, if desired.

-- IPv4/IPv6 dual-stack : Allocation of IPv4 and IPv6 addresses to Pods and Services.

-- Designed for extensibility : Add features to your Kubernetes cluster without changing upstream source code.

# Kubernetes - Architecture

<img width="1335" height="948" alt="image" src="https://github.com/user-attachments/assets/82c9e562-8cf6-4347-906f-65b9ee7ca782" />

A Kubernetes cluster consists of a control plane plus a set of worker machines, called nodes, that run containerized applications. Every cluster needs at least one worker node in order to run Pods.
The master node (a.k.a. control plane) is the brain of the Kubernetescluster. It manages the cluster's overall state, ensuring that the desired state(as defined by the user) matches the actual state of the cluster. The control
plane components take care of all the operational and administrative tasks. Worker nodes are the machine(s) where the actual application workloads (pods) run. They are responsible for running the containers and
ensuring that the application remains highly available, fault tolerant, and highly scalable.

# Control Plane Components

<img width="1037" height="802" alt="image" src="https://github.com/user-attachments/assets/362802e0-cbfc-4dbc-b1c6-d759929a46d9" />

-- API SERVER: It acts as the frontend for the Kubernetes control plane, and the client interacts with the cluster using API Server. It is responsible for validating and processing API requests, maintaining the desired state of the cluster, and handling Kubernetes resources such as pods, services, replication controllers, and others. API Server is the only control plane component that interacts with all other control plane components such as Scheduler, ETCD, Controller Manager, etc.

-- Kube-Scheduler: The Scheduler in Kubernetes is a component responsible for scheduling workloads (such as pods) to the nodes in the cluster. It watches for newly created pods with no assigned node, selects an appropriate node for each
pod, assigns a rank to the node, and then binds the pod to that node. The scheduler considers factors such as resource requirements, hardware/software constraints, affinity and anti-affinity specifications, labels and selectors, and
other policies defined by the user or cluster administrator when making scheduling decisions.

-- Controller Manager: The Controller Manager in Kubernetes is a component of the control plane that manages different types of controllers to regulate the state of the cluster and perform cluster-wide tasks. Each controller in the Controller Manager manages a specific aspect of the cluster's desired state, such as ReplicaSetController, DeploymentController, NamespaceController, NodeControllers, and others. These controllers continuously work to ensure that the current state of the cluster matches the desired state specified by users or applications. They monitor the cluster state through the Kubernetes API Server, detect any differences between the current and desired states, and take
corrective actions to reconcile them, such as creating or deleting resources as needed. For instance, if a node becomes NotReady (Unhealthy), the NodeController takes the action of node repair and replaces it with a healthy node (if required).

-- ETCD Server: ETCD is a distributed key-value storage used as the primary datastore in Kubernetes for storing cluster state and configuration information. It is a critical component of the Kubernetes control plane that is responsible
for storing information such as cluster configuration, the state of all Kubernetes objects (such as pods, services, and replication controllers), and information about nodes in the cluster.

-- CCM: In Kubernetes, the Cloud Controller Manager (CCM) is a control-plane component that lets Kubernetes talk to your cloud provider (AWS, Azure, GCP, etc.). It manages all the things that depend on cloud infrastructure, instead of hard-coding them into Kubernetes itself.
It runs controllers that handle cloud-specific tasks, mainly:

1️⃣ Node Controller

Checks if nodes (VMs) are still alive

If a VM is deleted in cloud (AWS EC2, Azure VM), it removes that node from the cluster

2️⃣ Service Controller

When you create a Service of type LoadBalancer:

    kind: Service
    spec:
      type: LoadBalancer


CCM asks the cloud provider to:

Create a real load balancer (ELB / ALB / Azure LB / GCP LB)

Attach it to your service

Manage health checks

3️⃣ Route Controller (some clouds)

Sets up network routes between nodes

Example: AWS VPC routes

4️⃣ Volume Controller (older versions, now CSI handles this)

Creates and attaches cloud disks:

AWS EBS

Azure Disk

GCP Persistent Disk

# Nodes
A Kubernetes node is nothing but a physical machine or a virtual machine with Kubernetes components installed on top of it and connected to form a Kubernetes cluster.

# Pod
In Kubernetes, a Pod acts as a logical wrapper around one or more containers, serving as the smallest unit of deployment.

In Docker, containers are often run using various command-line arguments (e.g., docker run -d -p...). The Pod wrapper replaces these manual commands with a declarative YAML file. This standardization allows DevOps engineers to:

• Store specifications in git repositories for better version control.

• Define all container requirements—such as image names, ports, and volume mounts—in a single, readable document.

• Make managing thousands of containers in production easier by having a clear "definition of how to run a container"

    minikube start --memory=2048 --driver=hyperkit
  
    kubectl config get-clusters
  
    kibectl config view
  
    kubectl get pods -o wide
  
    kubectl create -f pod.yml
  
    minikube ssh  or, ssh -i node_name/IP address
  
    curl IP_address
  
    kubectl logs nginx
  
    kubectl describe pod nginx

# Namespace: 
A namespace in Kubernetes provides a layer of isolation within a cluster, allowing you to separate objects and resources into distinct logical groups

Key characteristics of namespaces:
Resource Scoping: Most Kubernetes resources (like Pods, Services, and Deployments) belong to a namespace. Resource names must be unique within a namespace, but can be reused across different namespaces without conflict.

Isolation: Actions performed in one namespace do not affect resources in another. This prevents interference between different teams or environments sharing the same cluster.

Access Control: Namespaces are a key building block for managing security and access. Role-Based Access Control (RBAC) policies can be applied at the namespace level, ensuring users or teams only have access to their designated resources.

Resource Management: Administrators can use resource quotas to define and limit the aggregate CPU, memory, and storage consumption within a namespace, ensuring fair resource distribution and preventing a single project from monopolizing cluster resources.

DNS Naming: Services within the same namespace can use short names to communicate. To communicate across namespaces, you must use the fully qualified domain name (FQDN) in the format <service-name>.<namespace-name>.svc.cluster.local

Kubernetes begins with four namespaces:

default: The namespace for objects that have no other namespace.

kube-system: The namespace for Kubernetes-created objects.

kube-public: This namespace is generated automatically and can be accessed by all users (including those not authenticated). This namespace is mostly reserved for cluster use, in case some resources need to be publicly visible and readable across the entire cluster. This namespace’s public aspect is merely a convention, not a requirement.

kube-node-lease: This namespace contains Lease objects for each node. Node leases enable the kubelet to send heartbeats to the control plane, allowing it to detect node failure.

# Namespaces are easily created with the command:

$ kubectl create namespace <name>
A YAML file, like any other Kubernetes resource, can be created and used to create a namespace:

my-namespace.yaml: 

apiVersion: v1
kind: Namespace
metadata:
  name: <insert-namespace-name-here>
Then run:

$ kubectl create -f my-namespace.yaml
The command to display all namespaces in the cluster is:

$ kubectl get namespace

#  Worker Node Components

<img width="666" height="569" alt="image" src="https://github.com/user-attachments/assets/a5b1bbcd-7034-4ea0-8ba6-342f07cdacb4" />

Kubelet: In Kubernetes, Kubelet is the primary node agent that runs on each node in the cluster. It is responsible for managing the containers running on the node and ensuring that they are healthy and running as expected.

Some of the key responsibilities of Kubelet include
1. Pod Lifecycle Management: Kubelet is responsible for starting, stopping, and maintaining containers within a pod as directed by the Kubernetes API Server.
2. Node Monitoring: Kubelet monitors the health of the node and reports back to the Kubernetes control plane. If the node becomes unhealthy, the control plane can take corrective actions, such as rescheduling pods to other healthy nodes.
3. Resource Management: Kubelet manages the node's resources (CPU, memory, disk, etc.) and enforces resource limits and requests specified in pod configurations.
4. Volume Management: Kubelet manages pod volumes, including mounting and unmounting volumes as specified in the pod configuration.

kube-proxy: In Kubernetes, kube-proxy is a network proxy that runs on each node in the cluster. It is responsible for implementing part of the Kubernetes service concept, which enables network communication to your pods from network clients inside or outside of your cluster. Basically, it makes sure your traffic reaches the right Pod.
kube-proxy maintains network rules on each node. These network rules allow network communication to be forwarded to the appropriate pod based on IP address and port number.

Container Runtime: In Kubernetes, a container runtime is the software responsible for running containers. It is an essential component of the Kubernetes architecture because Kubernetes itself does not run containers directly; instead, it relies on a container runtime to do so.

Note Docker was the default container runtime for Kubernetes before Kubernetes version 1.24; however, the default container runtime has been changed to Containerd after 1.24 which is a CRI(container runtime interface) industry standard that provides a lightweight and reliable platform for managing containers.

# Service: 
In Kubernetes, a Service is a critical component that acts as a stable entry point for your applications. While a Deployment ensures your pods are running and auto-healing, a Service manages how those pods are accessed, solving the problem of ephemeral (temporary) IP addresses.
The sources break down the importance and functionality of Services into three primary categories:
1. Load Balancing
When you have multiple replicas of a pod to handle high traffic, you cannot expect users to know which individual pod IP to hit. A Service acts as a load balancer that sits on top of your pods.
• Traffic Distribution: It receives incoming requests and distributes them evenly across all available pod replicas.
• Stable Interface: Instead of using shifting pod IPs, users access the application via a single service name (e.g., payment.default.svc) or a stable Service IP address.
2. Service Discovery
Because pods are ephemeral, they are frequently destroyed and recreated with new IP addresses. If you manually tracked these IPs, your connection would break every time a pod restarted.
• Labels and Selectors: To solve this, Services do not track pods by IP addresses. Instead, they use a mechanism called labels and selectors.
• Automatic Updates: A Service is configured to watch for pods with a specific label (e.g., app: payment). Even if a pod dies and a new one is created with a different IP, as long as it has the correct label, the Service will automatically discover it and send traffic to it.
3. Exposing Applications (Service Types)
A Service determines who can access your application based on its Type. The sources define three default types:
• ClusterIP (Default): The application is only accessible inside the Kubernetes cluster. This is used for internal communication between services.
• NodePort: This exposes the application on a specific port of each worker node's IP. It allows anyone with access to your internal network or VPC to reach the application.
• LoadBalancer: This is used to expose the application to the external world (the internet). When used on a cloud provider like AWS, it triggers the creation of a public-facing Elastic Load Balancer (ELB) with a public IP address





