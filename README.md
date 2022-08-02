# kmmo-lab
Tests, docs and examples for different use cases of KMMO.

Different examples and YAML files to build in-cluster kernel module drivers, device plugins, load pre-built kernel modules with
KMMO (https://github.com/qbarrand/oot-operator)

Tests with :
- EKS Cluster in Amazon Web Services
- GKE Cluster in Google Cloud
- Vanilla Kubernetes with Ubuntu Nodes

# Notes on Elastic Kubernetes Service (EKS)
Taking for granted that EKS service at AWS should run by default Amazon Linux v2 nodes (Ubuntu could also be used and examples will be provided in such folder) examples include in-cluster builds (using and not using DKMS), device plugins and yet built driver containers.
As for today Kernel Management Module deploys at nodes labeled as node-role.kubernetes.io/master= but Control Plane (master) nodes do not allow workloads per design so user should label worker nodes with said label to make deploy work.

# Notes on Google Kubernetes Engine (GKE)
AutoPilot Clusters do limit what NodeSelectors and Linux Capabilities may be used in deployments, so deployments of KMMO in GKE platform should be done in standard clusters.
