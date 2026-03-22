# https://github.com/260078247/assignment-1-duduzile-trisha-mbhele.git

Name: Duduzile Trisha Mbhele
Student Number: 260078247

Repository: assignment-1-duduzile-trisha-mbhele

# Overview
This project demonstrates the deployment of a lightweight Kubernetes cluster using K3s on AWS EC2 instances. The objective is to provision infrastructure, configure a cluster, deploy applications, and document the process.

# System Requirements
| Component | Specification |
|-----------|--------------|
| Cloud Provider | AWS EC2 |
| Instance Type | t3.large |
| CPU | 2 vCPUs |
| RAM | 1 GB |
| Storage | 50 GB (EBS Volume) |
| Operating System | Ubuntu 24.04 |
| Kubernetes Distribution | K3s |

 # K3s Installation Steps - AWS
 
//bash
 
 # 1. Connect to EC2 Instance

export PS1="assignment-1-duduzile-k3s-server@ip-98.81.2.20:~$"

export PS1="assignment-1-duduzile-k3s-agent@ip-34.229.188.210:~$"

# Update System Packages on instances

#agent: sudo apt update -y

#server: sudo apt update -y

# Install K3s (Control Plane)

curl -sfL https://get.k3s.io | sh -

# Verify Node

kubectl get nodes

# Verify Pods

kubectl get pods -A

# Verify Cluster

sudo kubectl get nodes

# HELM DEPLOYMENT

# Install helm

curl https://raw.githubusercontent.com/helm/helm/main/scripts/get-helm-3 | bash

 # Deploy Nginx
 
sudo chmod 644 /etc/rancher/k3s/k3s.yaml

export KUBECONFIG=/etc/rancher/k3s/k3s.yaml

kubectl get nodes

helm repo add bitnami https://charts.bitnami.com/bitnami

helm repo update
helm install my-nginx bitnami/nginx
kubectl get pods

# Architectural Explanation

# What is K3s, and why is it used?
K3s is a lightweight, fully compliant Kubernetes distribution aimed at situations with low resources, such as edge computing, IoT, and development environments. Unlike normal Kubernetes, K3s is packed as a single binary and eliminates redundant components, making it faster to install and operate.
K3s is utilized in this project because it facilitates Kubernetes deployment on AWS EC2 instances while retaining all core Kubernetes functionality such as container orchestration, scalability, and service management. It is suited for learning and small-scale production environments because to its low resource usage and simple configuration needs.

This node manages the cluster, schedules workloads, and maintains cluster state. It includes components such as the API server, scheduler, and controller manager.
# Worker Node (Agent):
This node runs application workloads inside containers. It communicates with the control plane and executes assigned tasks.
# Container Runtime:
K3s uses containerd to run containers efficiently.
# Networking (CNI):
K3s includes a default networking solution that enables communication between pods across nodes.
# Ingress Controller:
Traefik is deployed by default in K3s to handle incoming traffic and expose services.
# Storage:
Local-path provisioner is used for dynamic storage provisioning.
This architecture is suitable for scalable and distributed applications, and mirrors real-world Kubernetes environments in a simplified way.

# Cluster Verification
# Nodes
![Nodes Output](Screenshots/agent-nodes1.png)
![Nodes Output](Screenshots/server-nodes.png)

# Pods
![Pods Output](Screenshots/agent-pods.png)
![Pods Output](Screenshots/server-pods.png)

# running instances
![instances Output](Screenshots/ec2-instances-agent-server.png)
![ubuntu-sos Output](Screenshots/ec2-ubuntu-agent.png)
![ubuntu-sos Output](Screenshots/ec2-ubuntu-server1.png)

# Deployment verification
![deployment Output](Screenshots/agent-deployment.png)
![deployment Output](Screenshots/server-deployment.png)

# Reflection
In this assignment, I learned how to deploy and manage a lightweight Kubernetes cluster using k3s on AWS. I gained practical experience in provisioning EC2 instances, configuring security groups, and setting up the necessary environment for a distributed system. I also learned how the k3s control plane (server) and worker nodes (agents) communicate, and how workloads are scheduled across the cluster. In addition, I improved my understanding of using Helm for application deployment and how Kubernetes resources such as pods and nodes are managed using kubectl commands. This helped me better understand how container orchestration works in real-world cloud environments.
During the assignment, I faced several challenges. One major issue was with Helm deployment, where I encountered errors related to cluster connectivity and configuration. In some cases, kubectl commands failed due to kubeconfig permission issues. I resolved this by correctly setting the KUBECONFIG environment variable and adjusting file permissions to allow proper access. Another challenge was embedding screenshots into my GitHub README file. Initially, the images did not display correctly because of incorrect paths or formatting. I resolved this by storing the images within the repository and using proper Markdown syntax with relative file paths. I also struggled with organizing my repository structure, particularly creating and linking a README folder, but I improved this by carefully structuring directories and verifying links before committing changes.
k3s is closely related to production Kubernetes but is designed to be more lightweight and easier to install. While traditional Kubernetes clusters are often complex and resource-intensive, k3s reduces overhead while maintaining compatibility with Kubernetes APIs. This makes it suitable for edge computing and environments with limited resources. In cloud-native and 5G architectures, k3s supports the deployment of distributed applications that require low latency, scalability, and high availability, which are critical in modern telecom and microservices-based systems.
Virtualization and containerization play a key role in enabling scalable services. Virtualization allows multiple virtual machines to run on a single physical server, improving resource utilization. Containerization, on the other hand, packages applications and their dependencies into lightweight, portable units that can run consistently across different environments. Together, they enable efficient resource allocation, rapid deployment, scalability, and isolation of services, which are essential for building and managing modern cloud-native applications.
 
# Conclusion
This project successfully demonstrated the deployment of a K3s cluster on AWS, including node configuration, application deployment using Helm, and validation through command outputs and screenshots.
