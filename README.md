# KMMO-LAB 
Examples for different use cases of KMM.

Examples and YAML files include in-cluster builds, device plugins and load of existing driver containers with KMMO (https://github.com/qbarrand/oot-operator)

Platforms :
- EKS Cluster in Amazon Web Services
- GKE Cluster in Google Cloud
- Vanilla Kubernetes with Ubuntu Nodes

## Notes on Elastic Kubernetes Service (EKS)

Elastic Kubernetes Service(EKS) at AWS run by default worker nodes based on Amazon Linux v2 (Ubuntu and maybe others could also be used and examples will be provided in such directory).
Kernel Management Module deploys at nodes labeled as `node-role.kubernetes.io/master=` but Control Plane (master) in EKS nodes do not allow custom workloads per design as these nodes are managed by AWS.
So as a user workaround we could label worker nodes with said key to make deploy work.

As underlying OS in nodes is https://github.com/awslabs/amazon-eks-ami which is based in Amazon Linux v2, using amazonlinux images as builder images is the easiest way to match kernel versions between hosts and builders. Also Amazon Linux repositories keep a pretty extensive package archive of different headers versions which is really useful when dealing with not so updated EKS nodes.

At sometime in a near future AL2022 wil be released as an official Amazon Linux OS. It will be based on Fedora Linux and will have SELinux enabled by default so probably changes should be made to examples accordingly:
[Amazon Linux 2022](https://docs.aws.amazon.com/linux/al2022/release-notes/planned-changes.html)

EKS Linux AMI versions always stick with a specific kernel version that can be checked [here](https://github.com/awslabs/amazon-eks-ami/blob/master/CHANGELOG.md).

These are Kernel and other relevant software versions for EKS AMI Linux from Kubernetes 1.22:

**VERSIONS** 
|     AMI               |kubelet| Docker	 |            Kernel	     |   Packer	 |       containerd   |
|---------------        |-------|----------------|---------------------------|-----------|--------------------|
|1.22.9-20220629	|1.22.9	|20.10.13-2.amzn2|	5.4.196-108.356.amzn2|	v20220629|	1.4.13-3.amzn2|
|1.22.9-20220620	|1.22.9	|20.10.13-2.amzn2|	5.4.196-108.356.amzn2|	v20220620|	1.4.13-3.amzn2|
|1.22.9-20220610	|1.22.9	|20.10.13-2.amzn2|	5.4.196-108.356.amzn2|	v20220610|	1.4.13-3.amzn2|
|1.22.6-20220526	|1.22.6	|20.10.13-2.amzn2|	5.4.190-107.353.amzn2|	v20220526|	1.4.13-2.amzn2.0.1|
|1.22.6-20220523	|1.22.6	|20.10.13-2.amzn2|	5.4.190-107.353.amzn2|	v20220523|	1.4.13-2.amzn2.0.1|
|1.22.6-20220429	|1.22.6	|20.10.13-2.amzn2|	5.4.188-104.359.amzn2|	v20220429|	1.4.13-2.amzn2.0.1|
|1.22.6-20220421	|1.22.6	|20.10.13-2.amzn2|	5.4.188-104.359.amzn2|	v20220421|	1.4.13-2.amzn2.0.1|
|1.22.6-20220420	|1.22.6	|20.10.13-2.amzn2|	5.4.188-104.359.amzn2|	v20220420|	1.4.13-2.amzn2.0.1|
|1.22.6-20220406	|1.22.6	|20.10.13-2.amzn2|	5.4.181-99.354.amzn2|	v20220406|	1.4.13-2.amzn2.0.1|
|1.22.6-20220317	|1.22.6	|20.10.7-5.amzn2|	5.4.181-99.354.amzn2|	v20220317|	1.4.6-8.amzn2|

## Notes on Google Kubernetes Engine (GKE)

AutoPilot Clusters do limit which NodeSelectors and Linux Capabilities may be used in deployments, so deployments of KMMO in GKE platform should be done in standard clusters.
In Standard GKE clusters Control Plane (master) is administered by Google so labeling and/or user workloads are not allowed in those nodes. Therefore labeling a worker node as `node-role.kubernetes.io/master=` is needed before deploying the controller manager.

Underlying OS in nodes running at GKE is Container-Optimized OS by default but it could be Ubuntu also.


## Notes on Ubuntu Bare Metal Cluster

Examples in Ubuntu directory are based on a bare-metal cluster with Ubuntu 22.04 LTS nodes. 


