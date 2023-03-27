# hranalytics-infrastructure

infrastructure project for hranalytics

# Prequisites

For each subscription a backend-rg with a key vault and storage account needs to be created.

- Storage account
  - This contains the tenant container where the state will be stored.
  - the storage access key will need to be uploaded in the key vault (see the tfplan script for naming conventions used).
- Key vault
  - This will contain various secrets in the form of ssh keys and ids.
- Service principal for terraform
  - A service principal needs to be created for terraform to use when deploying. Client ID, client secret and object ID needs to be uploaded to the key vault(see tfplan for naming convetions used)
- Service principal for dns
  - A service principal for DNS handling needs to be created. Client ID, client secret, object id and tenant id needs to be uploaded to the key vault(see the environment.tf file for naming conventions used)

# What it does.

The project contains the following modules:

- Network
  - Contains the resources like vnets, subnets, peering, public ips, network association and setting of roles
- Nodes
  - Contains the resources like virtual machines, sshkeys, network security group, network interface cards and disks

Environments:

- environment.tf
  - Contains loading of modules, creation of resource group and key vault data streams.
- env/environment.tfvars

  - Environment spesific variables, here you will need to config variables for the spesific environment.

# The project contains the following environments:

- Dev
- Playground
- Prod

The project creates a network with public IPs and linux vms, 4 total nodes are hardcoded into the locals.tf files withing each module and one and each can be enabled in the <environment>.tfvars file there is also an option to enable backup resources, this will also enable an additional vnet and subnet aswell as peering between the two vnets.
Peering of networks is also created if backup is enabled.
the private keys is uploaded to a key vault.
