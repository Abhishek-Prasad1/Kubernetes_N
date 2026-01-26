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
  minikube ssh  or, cluster_IP_address ssh
  curl IP_address
  kubectl logs nginx
  kubectl describe pod nginx
  



