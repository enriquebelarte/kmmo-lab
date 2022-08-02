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

# Notes on Google Kubernetes Engine (GKE)
AutoPilot Clusters do limit what NodeSelectors and Linux Capabilities may be used in deployments, so deployments of KMMO in GKE platform should be done in standard clusters.
