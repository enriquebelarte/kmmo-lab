# Kernel Module Management Lab 

Kernel Module Management a.k.a KMM manages out of tree kernel modules in Kubernetes.

By installing the controller in a Kubernetes cluster we will get a new NameSpace where a Deployment will run and create a ReplicaSet.

Once the ReplicaSet is running we can create and use a new Module object which will manage the build and/or run of a kernel module.

In this document we will find examples and YAML files including in-cluster module building, device plugins and use of module loaders with KMM (https://github.com/qbarrand/oot-operator) 

## Installation

### Command line:

``kubectl apply -k https://github.com/qbarrand/oot-operator/config/default``

### Operator Hub

TO-DO

## Platforms :
- EKS Cluster in Amazon Web Services
- GKE Cluster in Google Cloud Platform
- Vanilla Kubernetes with Ubuntu Nodes

###  Elastic Kubernetes Service (EKS)

Elastic Kubernetes Service(EKS) at AWS run by default worker nodes based on Amazon Linux v2 (Ubuntu and maybe others could also be used and examples will be provided in such directory).
Kernel Management Module deploys at nodes labeled as `node-role.kubernetes.io/master=` or `node-role.kubernetes.io/control-plane=` depending on which Kubernetes version we are running, but Control Plane (master) in EKS nodes do not allow custom workloads per design as these nodes are managed by AWS.
So as a user workaround we could label worker nodes with said key to make deployment work.

As underlying OS in nodes is [Amazon EKS Linux](https://github.com/awslabs/amazon-eks-ami) which is based in Amazon Linux v2, using amazonlinux images as builder images is the easiest way to match kernel versions between hosts and builders. Also Amazon Linux repositories keep a pretty extensive package archive of different headers versions which is really useful when dealing with not so updated EKS nodes.

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

### Google Kubernetes Engine (GKE)

AutoPilot Clusters do limit which NodeSelectors and Linux Capabilities may be used in deployments, so deployments of KMMO in GKE platform should be done in standard clusters.
In Standard GKE clusters Control Plane (master) is administered by Google so labeling and/or user workloads are not allowed in those nodes. Therefore labeling a worker node as `node-role.kubernetes.io/master=` is needed before deploying the controller manager.

Underlying OS in nodes running at GKE is Container-Optimized OS by default but it could be Ubuntu also.

** KMM labels nodes with Kernel version.
 In Container Optimized OS (COS) used at GKE nodes the kernel version ends in a plus sign (i.e 5.10.109+). This is an issue when controller tries to label nodes as Kubernetes labels ending in symbols are not allowed.
 (Workaround should be found)



[WIP section]

### Ubuntu Bare Metal Cluster

Examples in [ubuntu](ubuntu) directory are based on a bare-metal cluster with Ubuntu 22.04 LTS nodes. 

[WIP section]


