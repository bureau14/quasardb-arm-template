# Install a QuasarDB cluster on Ubuntu Virtual Machines using Custom Script Linux Extension

This template deploys a QuasarDB cluster on Ubuntu virtual machines. This template also provisions a storage account, virtual network, availability sets, public IP addresses and network interfaces required by the installation.

The example expects the following parameters:

| Name   | Description    |
|:--- |:---|
| adminUsername  | Admin user name for the Virtual Machines  |
| adminPassword  | Admin password for the Virtual Machines  |
| storageAccountPrefix  | Unique DNS Name for the Storage Account where the Virtual Machine's disks will be placed (multiple storage accounts are created with this template using this value as a prefix for the storage account name) |
| region | Region name where the corresponding Azure artifacts will be created |
| virtualNetworkName | Name of the Virtual Network that is created and that resources will be deployed in to |
| clusterName | The name of the new cluster that is provisioned with the deployment |
| tshirtSize | Higher level definition of a cluster size. It can take Small, Medium and Large values. This value causes cluster sizes with following characteristics. Small: 3xStandard_A2, Medium: 4xStandard_A6, Large: 5xStandard_D14  |
| vmNamePrefix | The prefix for the names of the VMs that will be provisioned |
| qdbPackageDownloadBase | The URL base the QuasarDB package is downloaded from |
| qdbPackage | The QuasarDB package name |
| jumpbox | Deploys two VMs, one Ubuntu, one Windows to access the cluster from the Internet |

## Topology

This template deploys a configurable number of cluster nodes of a configurable size.  The cluster nodes are internal and only accessible on the virtual network.  The cluster can be accessed through an Ubuntu VM ("jumpbox") accessible via SSH (port 22) on a public IP, for test purposes only. The assumption for the deployment is, the cluster is going to be provisioned as the back end of a service, and never be exposed to internet directly.

The cluster is deployed to one single availability set to ensure the distribution of VMs accross different update domains (UD) and fault domains (FD).

## Known Issues and Limitations

