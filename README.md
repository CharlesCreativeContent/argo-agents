# How to deploy Argo Agents on AWS EKS

Managing Kubernetes clusters on Amazon EKS can be challenging, particularly when it comes to achieving efficient continuous deployment and managing applications at scale. The complexity of ensuring seamless operations, updates, and security often overwhelms even seasoned DevOps teams. This is where Akuity steps in, offering a streamlined solution with its EKS add-on, making cluster management more efficient and secure.

## Technical Value of Akuity Agents

Akuity Agents enhance Amazon EKS by providing an integrated solution for continuous deployment and cluster management.

Key benefits include:

- **Simplified Deployment:** Automate and streamline application deployment with Argo CD integration.
- **Enhanced Security:** Secure your deployments with managed secrets and policies.
- **Scalability:** Effortlessly manage and scale your Kubernetes clusters with robust tools and integrations.
- **Reduced Complexity:** Simplify cluster management through a single platform, reducing the learning curve and operational overhead.

## How to Install and Use Akuity Agents on Amazon EKS

### Prerequisites:

- An Akuity Platform account with an Argo CD instance
- An AWS EKS cluster
- Subscription to the Akuity Agent EKS add-on
- kubectl and AWS CLI installed

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

4. Install via CLI:

```bash
export AKP_API_URL="<The URL you got from AKP>"
aws eks create-addon --cluster-name my-cluster --addon-name akuity_agent \
   --configuration-values "{\"akpUrl\":\"$AKP_API_URL\"}" --resolve-conflicts OVERWRITE
```

5. Create API Token Secret:


```bash
export TOKEN=<your cluster token>
kubectl create secret generic akuity-platform-api-token -n akuity --from-literal=AKP_TOKEN="$TOKEN"
```

6. Verify Installation:


```bash
aws eks describe-addon --addon-name akuity_agent --region <AWS_REGION> --cluster-name <CLUSTER_NAME>
```

7. Clean Up:

```bash
kubectl delete secret akuity-platform-api-token -n akuity
```

## Summary
Using Akuity Agents on Amazon EKS simplifies the management and deployment of applications, enhances security, and scales operations efficiently. By integrating with Argo CD and providing robust automation tools, Akuity empowers DevOps teams to focus on innovation rather than infrastructure management.

## Call to Action:

Ready to streamline your Kubernetes management? Get started with Akuity on Amazon EKS today and transform your DevOps workflow!
