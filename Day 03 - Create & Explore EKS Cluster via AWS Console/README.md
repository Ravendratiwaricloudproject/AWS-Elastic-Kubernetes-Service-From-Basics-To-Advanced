# Amazon Elastic Kubernetes Service (EKS) Cluster:

EKS Cluster is a group of Nodes working together to manage and run containerized applications.

# EKS control plane:

• The Control Plane is the management layer of Kubernetes that controls the entire cluster. It is often called the brain of Kubernetes because it makes decisions about the cluster.

• The Control Plane manages cluster state and ensures the system behaves as expected.

• EKS runs a single tenant Kubernetes control plane for each cluster, and control plane infrastructure is not shared across clusters or AWS accounts.

• This control plane consists of at least two API server nodes and three etcd nodes that run across three Availability Zones within a Region.

• EKS automatically detects and replaces unhealthy control plane instances, restarting them across the Availability Zones within the Region as needed.

# Data plane, Worker node & node group:

- Data Plane:

• The data plane is responsible for running your applications (pods) and handling actual workload execution.

• worker nodes are the main components of the data plane.

• Everything that runs your workloads called Data plane.

• Data Plane managed by you or AWS depending on mode (EC2 worker nodes OR Fargate).

- Worker Node:

• Worker machines in Kubernetes are called nodes.  These are EC2 Instances.

• A node or worker node is a physical or virtual machine (e.g., EC2 instance) that runs your workloads in the form of pods.

• EKS worker nodes run in our AWS account and connect to our cluster's control plane via the cluster API server endpoint.

- Node Group: A node group is one or more EC2 instances that are deployed in an EC2 Autoscaling group.

All instances in a node group must:

• Be the same instance type

• Be running the same AMI

• Use the same EKS worker node IAM role

# Fargate & Fargate profile (Serverless):

- Fargate:

• Fargate is a serverless compute engine provided by Amazon Web Services. It runs your containers (pods) without EC2 instances.

• AWS Fargate provides on-demand, right-sized compute capacity for containers.

• With Fargate, we no longer have to provision, configure, or scale groups of virtual machines to run containers.

• Each pod running on Fargate has its own isolation boundary and does not share the underlying kernel, CPU resources, memory resources, or elastic network interface with another pod.

Note: In EKS Fargate mode, DaemonSets, privileged containers, host-level access, and EBS-backed persistent volumes are not supported because Fargate abstracts the underlying nodes. It is best suited for serverless and stateless workloads rather than high-performance or infrastructure-level workloads.

- Fargate profiles:

• A Fargate Profile is a configuration rule inside EKS. It tells Kubernetes Which pods should run on Fargate.

• AWS specially built Fargate controllers that recognizes the pods belonging to Fargate and schedules them on Fargate profiles.

• We will see more in our Fargate learning section.

# VPC:

• A Virtual Private Cloud (VPC) in AWS is a logically isolated virtual network inside the AWS cloud where you can launch and manage AWS resources securely.

• In simple terms, a VPC is your own private network inside AWS.

• EKS uses AWS VPC network policies to restrict traffic between control plane components to within a single cluster.

• Control plane components for a EKS cluster cannot view or receive communication from other clusters or other AWS accounts, except as authorized with Kubernetes RBAC policies.

• This secure and highly-available configuration makes EKS reliable and recommended for production workloads.


# What is kubeconfig file in EKS?

A kubeconfig file is a YAML configuration file used by kubectl to connect and authenticate to a Kubernetes cluster.

It tells kubectl:

Which Kubernetes cluster to connect to

How to authenticate

Which user and context to use

It is usually stored at:
~/.kube/config

# What Does kubeconfig Contain?

It mainly contains 3 sections:

1️⃣ Cluster Information

• API Server endpoint URL 

• CA certificate data

2️⃣ User Information

• Authentication method 

• Token or IAM exec command (for EKS)

3️⃣ Context

Context connects:

• Cluster 

• User 

• Namespace

# Why Do We Need kubeconfig?

Without kubeconfig:

• kubectl does not know

o Which cluster to connect to 

o What API server endpoint to use

o How to authenticate

o Which certificate to trust

So kubeconfig acts like a connection profile.

- Generate kubeconfig file:

aws eks update-kubeconfig --name <cluster-name> --region <region>
 

 
# What is Add-ons in EKS?

 It is not a part of the core EKS components.

In EKS, addons are additional components or tools that extend the functionality of a EKS cluster. They are not part of the core EKS system, but they provide features that are often needed in real-world cluster operations, such as networking, monitoring, logging, or DNS.

Addons use EKS resources (DaemonSet, Deployment, etc) to implement cluster features. Because these are providing cluster-level features, namespaced resources for addons belong within the kube-system namespace.

Common Types of EKS Addons:

1. VPC CNI Plugin

2. Kube-proxy

3. Core DNS

4. Metrics server

5. Pod Identity Agent

And many more.


# What is EKS Observability?

EKS Observability refers to the ability to monitor, measure, analyze, and understand what is happening inside your Amazon Elastic Kubernetes Service (EKS) cluster.
