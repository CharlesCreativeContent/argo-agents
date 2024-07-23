# How to deploy Argo Agents on AWS EKS

Managing Kubernetes clusters on Amazon EKS can be challenging, particularly when it comes to achieving efficient continuous deployment and managing applications at scale. The complexity of ensuring seamless operations, updates, and security often overwhelms even seasoned DevOps teams. This is where Akuity steps in, offering a streamlined solution with its EKS add-on, making cluster management more efficient and secure.

## Technical Value of Akuity Agents

Akuity Agents enhance Amazon EKS by providing an integrated solution for continuous deployment and cluster management. Key benefits include:

Simplified Deployment: Automate and streamline application deployment with Argo CD integration.
Enhanced Security: Secure your deployments with managed secrets and policies.
Scalability: Effortlessly manage and scale your Kubernetes clusters with robust tools and integrations.
Reduced Complexity: Simplify cluster management through a single platform, reducing the learning curve and operational overhead.

## How to Install and Use Akuity Agents on Amazon EKS

### Prerequisites:

An Akuity Platform account with an Argo CD instance
An AWS EKS cluster
Subscription to the Akuity Agent EKS add-on
kubectl and AWS CLI installed

### Steps to Install:

1. Add an EKS Cluster to Argo CD:

- Navigate to Argo CD → your instance → Clusters.

- Click + Connect a cluster and input your Cluster Name.

- Expand the "Advanced settings" and select the "Addons" tab.

- Click + Add for EKS Add-on and then Connect Cluster.


2. Create the akuity Namespace:

 ```bash
kubectl create namespace akuity
```

3. Install via AWS Console:
   
- Go to the EKS cluster in the AWS console.

- Navigate to the add-ons tab and select Get more add-ons.
  
- Find and select Akuity Agent and follow the prompts to complete the installation.

