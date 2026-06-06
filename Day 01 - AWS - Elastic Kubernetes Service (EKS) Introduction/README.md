                     ########  AWS - Elastic Kubernetes Service (EKS) Introduction  ########


# What is Kubernetes?

Kubernetes is an open-source container orchestration tool that automates the deployment, scaling, and management of containerized applications.

Kubernetes originally designed by Google, the project in now maintained by the Cloud Native Computing Foundation (CNCF).

Kubernetes was announced by Google in June 2014

Kubernetes written in "Go" language.

Go language is called Golang language.

Since Kubernetes is an open-source container orchestration platform, major cloud providers offer their own managed Kubernetes services based on the open-source Kubernetes project.

All these Cloud Provider, use the open-source Kubernetes project and provide managed services around it, adding features such as cluster management, networking, load balancing, security, monitoring, and autoscaling.

Examples:

AWS – Amazon EKS (Elastic Kubernetes Service)

Microsoft Azure – AKS (Azure Kubernetes Service)

Google Cloud – GKE (Google Kubernetes Engine)


# What is Amazon EKS (Elastic Kubernetes Service)?

Amazon EKS is a managed Kubernetes service that makes it easy to run Kubernetes on AWS without managing the control plane. AWS manages the control plane infrastructure, ensuring high availability and scalability, while you manage the data plane (worker nodes) and workloads (unless using features like EKS Auto Mode or Fargate).

Amazon EKS simplifies building, securing, and maintaining Kubernetes clusters. There are two operational models (approaches) in Amazon EKS based on how AWS manages the cluster. That means, we have two ways to use/manage/operate EKS are as follows:

• EKS standard: Using the EKS standard feature, AWS manages the Kubernetes control plane and data plane (worker node & node group) managed by you.

• EKS Auto Mode: Using the EKS Auto Mode feature, AWS manages the Kubernetes control plane & data plane both. It simplifies Kubernetes management by automatically provisioning infrastructure, selecting optimal compute instances, dynamically scaling resources, continuously optimizing costs, patching operating systems, and integrating with AWS security services.

Amazon EKS Capabilities - Building and scaling with Kubernetes:

Amazon EKS not only helps you manage Kubernetes clusters but also helps you build and scale application systems. It provides fully managed capabilities that extend Kubernetes with built-in, hands-free tools including:

• Argo CD: Argo CD provides declarative, GitOps-based continuous deployment for your workloads, AWS resources, and cloud infrastructure.

• AWS Controllers for Kubernetes (ACK): ACK enables Kubernetes-native creation and lifecycle management of AWS resources, unifying workload orchestration and Infrastructure-as-code workflows.

• kro (Kube Resource Orchestrator): kro extends native Kubernetes features to simplify custom resource creation, orchestration, and compositions, giving you the tools to create your own customized cloud building blocks.

Note: EKS Capabilities are cloud resources that minimize the operational burden of installing, maintaining, and scaling these foundational platform components in your clusters, letting you focus on building software rather than cluster platform operations.

# Features of Amazon EKS:

Amazon EKS provides a fully managed Kubernetes experience with the following key features:

• Management Interfaces: Multiple ways to create and manage clusters including AWS Management Console, Amazon EKS API/SDKs, CDK, AWS CLI, eksctl CLI, AWS CloudFormation, and Terraform.

• Access Control: Secure access using AWS IAM and Kubernetes RBAC integration.

• Compute Resources: Supports EC2 instances including Graviton and Nitro for optimized performance.

• Storage Options: Integrates with EBS, EFS, S3, FSx, and CSI drivers for flexible storage.

• Security: Follows a shared responsibility model with strong AWS security integration.

• Monitoring & Observability: Use the observability dashboard to monitor Amazon EKS clusters. Monitoring tools include   Prometheus, CloudWatch, CloudTrail, and ADOT Operator. For more information on dashboards, metrics servers, and other tools.

• Managed Cluster Capabilities: AWS handles scaling, patching, and core Kubernetes components. 

• Kubernetes compatibility and support: Amazon EKS is certified Kubernetes-conformant, so you can run Kubernetes applications without modification and use community tools and plugins. It also provides standard and extended support for Kubernetes versions.

# What is Control Plane in Kubernetes?

The Control Plane is the management layer of Kubernetes that controls the entire cluster. It is often called the brain of Kubernetes because it makes decisions about the cluster. The Control Plane manages cluster state and ensures the system behaves as expected.

We can say that:

The Control Plane is a collection of multiple software components that together manage the Kubernetes cluster.

# What is Data Plane?

The Data Plane is the worker layer where application workloads run.

It is the part of the cluster where:

•	Containers execute 

•	Applications run 

•	Traffic is handled 

The Control Plane manages and makes decisions for the worker nodes, and the Data Plane executes those decisions.

Note: The Control Plane and the Data Plane are architectural layers (logical parts) of the Kubernetes cluster — they are not single software programs.


# Control Plane Components:

1. kube-apiserver:

The kube-apiserver is the core component that exposes the Kubernetes HTTP API.
It is used for all communication within the cluster and performs all actions on cluster resources.
It serves as the main entry point to the cluster.
The kube-apiserver authenticates and validates every request before processing it.

2. etcd:

Consistent and highly-available key value store for all API server data.
Its contain all the cluster information.

3. (Scheduler) kube-scheduler:

Its decide and schedule right node for the pods.

4. controller-manager (kube-controller-manager):

Note: Controller Manager is just a short/common name people use instead of saying the full: kube-controller-manager
The controller manager (kube-controller-manager) is like the brain of the Kubernetes control plane that runs various controllers and monitors the state of the cluster. It ensures that the cluster’s desired state matches the actual state by continuously taking necessary actions.

The kube-controller-manager is the actual Kubernetes core control plane component. It manages and runs multiple controllers, such as:

• Node Controller 

• ReplicaSet Controller

• Deployment Controller 

• Job Controller 

• Endpoint Controller

• and many more

All these controllers together give Kubernetes its core strengths:

• Self-healing 

• Auto-scaling 

• Rolling updates 

• High availability 

• Fault tolerance

Without controllers → Kubernetes would just be an API server storing YAML.
Controllers are what make Kubernetes dynamic and automated.

1. Node Controller:

Purpose:

Monitors the health status and availability of worker nodes.

What it does:

• Detects if a node becomes unreachable

• Marks node as NotReady 

• Evicts pods after timeout

Why it’s useful:

Ensures workloads are not stuck on failed machines.

Example: If a node goes down, it takes necessary action, such as marking it as unreachable and triggering replacement if needed.

2. ReplicaSet Controller:

Purpose:

Monitors the status of pods and ensures the desired number of replicas are running.

What it does:

• Creates pods if count is low 

• Deletes extra pods if count is high

Why it’s useful:

Provides self-healing and scaling.

Example: If a pod crashes or is deleted, it will create a new pod to maintain the desired count.

3. Deployment Controller:

Purpose:

Manages Deployments and rolling updates.

What it does:

• Creates and manages ReplicaSets 
• Handles rolling updates 
• Supports rollback

Why it’s useful:

Allows zero-downtime application updates.

Example:

You update image version → it replaces old pods with new ones.

4. Job Controller:

Purpose:

Manages batch jobs.

What it does:

• Creates pods to complete a task 
• Restarts failed job pods 
• Stops once job is completed

Why it’s useful:

Used for:

• Batch processing 
• Database migrations 
• Scheduled tasks
• Endpoint Controller:

Purpose:

Maintains Service-to-Pod mapping.

What it does:
• Updates endpoint list when pods are added/removed 
• Keeps Service routing accurate

Why it’s useful:

Ensures traffic is routed only to healthy pods.
Without it → Services wouldn’t know where to send traffic.


# Cloud-controller-manager:

The cloud-controller-manager connects Kubernetes to the cloud provider APIs. It is a External vendor coordinator (talks to AWS)
Its run in the control plane but, it is a separate component responsible for cloud-specific tasks.

It includes controllers such as:

• Node Controller – syncs node status with cloud provider 
• Route Controller – manages cloud network routes 
• Service Controller – manages cloud load balancers

The Cloud Controller Manager talks to cloud infrastructure APIs, Such as:

• Compute APIs (EC2) 
• Load Balancer APIs (NLB/ALB) 
• Storage APIs (EBS) 
• Network/VPC APIs (routes, zones) 
• and many more


# Data Plane Components:

Run on every node, maintaining running pods and providing the Kubernetes runtime environment:

1. kubelet:

It is responsible for all the activity in the worker node.    
 Kubelet runs on each worked node in the cluster. It makes sure that containers are running in a Pod.

2. kube-proxy:

Maintains network rules on nodes to implement Services. It enables network communication between Pods and Services, including load balancing traffic to the correct Pods.

3. Container Runtime Interface(CRI):

CRI is the interface that allows kubelet to communicate with container runtimes like containerd or CRI-O to manage  containers.
It is Software which is responsible for managing the execution and lifecycle of containers within the Kubernetes environment.


kubelet (CRI API calls) - Container Runtime (containerd / CRI-O) - Containers (Pods)

Note: Previously, we were using “Docker Engine container runtime” but now, it is no longer supported for standard AWS EKS clusters.


