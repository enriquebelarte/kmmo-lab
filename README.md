# kmmo-lab
Docs and examples for different use cases of KMMO.

Examples and YAML files include in-cluster builds (using and not using DKMS), device plugins and load of existing driver containers with KMMO (https://github.com/qbarrand/oot-operator)

Platforms :
- EKS Cluster in Amazon Web Services
- GKE Cluster in Google Cloud
- Vanilla Kubernetes with Ubuntu Nodes

# Notes on Elastic Kubernetes Service (EKS)
Taking for granted that EKS service at AWS should run by default Amazon Linux v2 nodes (Ubuntu could also be used and examples will be provided in such folder).
Kernel Management Module deploys at nodes labeled as 'node-role.kubernetes.io/master=' but Control Plane (master) in EKS nodes do not allow workloads per design as these nodes are managed by AWS so user should label worker nodes with said label to make deploy work.

As underlying OS in nodes is https://github.com/awslabs/amazon-eks-ami which is based in Amazon Linux v2, using amazonlinux images as builder images is the easiest way to match kernel versions between hosts and builders.

# Notes on Google Kubernetes Engine (GKE)
AutoPilot Clusters do limit which NodeSelectors and Linux Capabilities may be used in deployments, so deployments of KMMO in GKE platform should be done in standard clusters.
In Standard GKE clusters Control Plane (master) is administered by Google so it is not allowing labeling and/or user workloads. Therefore labeling a worker node as 'node-role.kubernetes.io/master=' is needed before deploying the controller manager.

Underlying OS in nodes running at GKE is Container-Optimized OS.
