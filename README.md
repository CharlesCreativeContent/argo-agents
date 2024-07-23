# How to deploy Akuity Agent on Amazon EKS

# Streamlining EKS Management with Akuity Agent

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

- An [Akuity Platform](https://akuity.cloud/) account with an Argo CD instance
- An AWS EKS cluster
- Subscription to the Akuity Agent EKS add-on
- kubectl and AWS CLI installed

> [!IMPORTANT]
> During EKS add-on installation, images must be pulled only from the EKS repository. This can’t be changed by the user.

### Steps to Install:

1. Add an EKS Cluster to Argo CD:

   - Navigate to Argo CD → your instance → Clusters.
   - Click + Connect a cluster and input your Cluster Name.
   - Expand the "Advanced settings" and select the "Addons" tab.
   - Click + Add for EKS Add-on and then Connect Cluster.

> [!NOTE]
> Refer to [documentation](https://docs.akuity.io/tutorials/eks-addon-agent-install/#create-the-akuity-namespace) for more details

2. Create the akuity Namespace:

 ```bash
kubectl create namespace akuity
```

<details>
<summary>
Install via AWS Console:
</summary>
<br>

   - Go to the EKS cluster in the AWS console.
   - Navigate to the add-ons tab and select Get more add-ons.
   - Find and select Akuity Agent and follow the prompts to complete the installation.

</details>

<details>
<summary>
Install via CLI:
</summary>
<br>

- **Install the Akuity Agent add-on** - In the Install Akuity Agent pop-up screen, enter the name of your EKS cluster
- click "Copy to Clipboard" on step 2.

<img src="https://docs.akuity.io/assets/images/eks_addon_akp_cluster_add_3-6176f1feefb71fe66c84c496660262db.png" alt="stuff">

- Paste the copied command into your terminal and run it to apply the agent manifest.

It will look something like this

```bash
export AKP_API_URL="<The URL you got from AKP>"
aws eks create-addon --cluster-name my-cluster --addon-name akuity_agent \
   --configuration-values "{\"akpUrl\":\"$AKP_API_URL\"}" --resolve-conflicts OVERWRITE
```

</details>


3. Create API Token Secret:


```bash
export TOKEN=<your cluster token>
kubectl create secret generic akuity-platform-api-token -n akuity --from-literal=AKP_TOKEN="$TOKEN"
```

4. Verify Installation:


```bash
aws eks describe-addon --addon-name akuity_agent --region <AWS_REGION> --cluster-name <CLUSTER_NAME>
```

5. Clean Up:

```bash
kubectl delete secret akuity-platform-api-token -n akuity
```

## Summary
Using Akuity Agents on Amazon EKS simplifies the management and deployment of applications, enhances security, and scales operations efficiently. By integrating with Argo CD and providing robust automation tools, Akuity empowers DevOps teams to focus on innovation rather than infrastructure management.

## Call to Action:

Ready to streamline your Kubernetes management? Get started with Akuity on Amazon EKS today and transform your DevOps workflow!
