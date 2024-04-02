1.  logeo en AZ
```
az login

az account set --subscription 612fefba-a432-4c2c-b0bb-7a788c71c69c
```

2. crear infra con tf
``` main.tf

######################## GENERAL ########################

  

resource "azurerm_resource_group" "main" {

name = "${var.prefix}-${var.environment}-rg"

location = var.location

}

###################### Networking ########################

  
  

resource "azurerm_virtual_network" "main" {

name = "${var.prefix}-${var.environment}-vnet"

resource_group_name = azurerm_resource_group.main.name

location = var.location

address_space = ["192.168.0.0/16"]

}

  

resource "azurerm_subnet" "service" {

name = "${var.prefix}-${var.environment}-service-subnet"

resource_group_name = azurerm_resource_group.main.name

virtual_network_name = azurerm_virtual_network.main.name

address_prefixes = ["192.168.1.0/24"]

}

  

resource "azurerm_subnet" "apps" {

name = "${var.prefix}-${var.environment}-apps-subnet"

resource_group_name = azurerm_resource_group.main.name

virtual_network_name = azurerm_virtual_network.main.name

address_prefixes = ["192.168.2.0/24"]

}

  

resource "azurerm_subnet" "gateway" {

name = "${var.prefix}-${var.environment}-gateway-subnet"

resource_group_name = azurerm_resource_group.main.name

virtual_network_name = azurerm_virtual_network.main.name

address_prefixes = ["192.168.3.0/27"]

}

  
  

resource "azurerm_public_ip" "main" {

name = "${var.prefix}-${var.environment}-public-ip"

resource_group_name = azurerm_resource_group.main.name

location = var.location

allocation_method = "Static"

sku = "Standard"

}

###################### Networking ########################

  
  

resource "azurerm_virtual_network" "main" {

name = "${var.prefix}-${var.environment}-vnet"

resource_group_name = azurerm_resource_group.main.name

location = var.location

address_space = ["192.168.0.0/16"]

}

  

resource "azurerm_subnet" "service" {

name = "${var.prefix}-${var.environment}-service-subnet"

resource_group_name = azurerm_resource_group.main.name

virtual_network_name = azurerm_virtual_network.main.name

address_prefixes = ["192.168.1.0/24"]

}

  

resource "azurerm_subnet" "apps" {

name = "${var.prefix}-${var.environment}-apps-subnet"

resource_group_name = azurerm_resource_group.main.name

virtual_network_name = azurerm_virtual_network.main.name

address_prefixes = ["192.168.2.0/24"]

}

  

resource "azurerm_subnet" "gateway" {

name = "${var.prefix}-${var.environment}-gateway-subnet"

resource_group_name = azurerm_resource_group.main.name

virtual_network_name = azurerm_virtual_network.main.name

address_prefixes = ["192.168.3.0/27"]

}

  
  

resource "azurerm_public_ip" "main" {

name = "${var.prefix}-${var.environment}-public-ip"

resource_group_name = azurerm_resource_group.main.name

location = var.location

allocation_method = "Static"

sku = "Standard"

}

############################### AKS #######################

  

resource "azurerm_kubernetes_cluster" "main" {

name = "${var.prefix}-${var.environment}-aks"

location = var.location

resource_group_name = azurerm_resource_group.main.name

dns_prefix = "${var.prefix}-${var.environment}-aks-dns"

oidc_issuer_enabled = true

role_based_access_control_enabled = true

identity {

type = "UserAssigned"

identity_ids = [azurerm_user_assigned_identity.main.id]

}

default_node_pool {

name = "default"

node_count = 1

vm_size = "Standard_D2s_v3"

enable_auto_scaling = true

max_count = 2

min_count = 1

vnet_subnet_id = azurerm_subnet.apps.id

}

linux_profile {

admin_username = var.username

ssh_key {

key_data = jsondecode(azapi_resource_action.ssh_public_key_gen.output).publicKey
}
}
network_profile {

network_plugin = "kubenet"

load_balancer_sku = "standard"
}
tags = {

Environment = var.environment

}
}
####################### Identity ###################

resource "azurerm_user_assigned_identity" "main" {

location = var.location

name = "${var.prefix}-${var.environment}-msi"

resource_group_name = azurerm_resource_group.main.name

}
############### ACR #################

resource "azurerm_container_registry" "main" {

name = "${var.prefix}${var.environment}acr"

resource_group_name = azurerm_resource_group.main.name

location = var.location

sku = "Standard"

admin_enabled = true

identity {

type = "UserAssigned"

identity_ids = [azurerm_user_assigned_identity.main.id]

}

tags = {

Environment = var.environment

}

}

####################### Storage ###################

resource "azurerm_storage_account" "main" {

name = "${var.prefix}${var.environment}sa"

resource_group_name = azurerm_resource_group.main.name

location = azurerm_resource_group.main.location

account_tier = "Standard"

account_replication_type = "GRS"

tags = {

environment = "${var.environment}"

}
}
######################## AKV ######################

resource "azurerm_key_vault" "main" {

name = "${var.prefix}-${var.environment}-kv"

location = azurerm_resource_group.main.location

resource_group_name = azurerm_resource_group.main.name

enabled_for_disk_encryption = true

tenant_id = "ce67aede-9a8e-4810-993a-395b1e08e530"

soft_delete_retention_days = 7

purge_protection_enabled = false

sku_name = "standard"

access_policy {

tenant_id = "ce67aede-9a8e-4810-993a-395b1e08e530"
object_id = "0e9cb019-0f53-4dba-96f1-cd3e2a565381"

key_permissions = [
"Get","Create","List"
]
secret_permissions = [
"Get","Set","List"
]
storage_permissions = [
"Get","Set","List"
]
}
}
```

```variables.tf
variable "location" {

description = "location of resources"

default = "eastus"

type = string

}  
variable "prefix" {

description = "name project"

default = "mmrv"

type = string

}

variable "environment" {

description = "ej. dev staging prod"

default = "staging"

type = string

}
variable "aks_service_cidr" {

description = "CIDR notation IP range from which to assign service cluster IPs"

default = "10.0.0.0/16"

}
variable "aks_dns_service_ip" {

description = "DNS server IP address"

default = "10.0.0.10"

}

variable "username" {

description = "admin use for node instances"

default = "aks-admin"

}
```

```ssh.tf
resource "random_pet" "ssh_key_name" {

prefix = "ssh"

separator = ""
}
  
resource "azapi_resource_action" "ssh_public_key_gen" {

type = "Microsoft.Compute/sshPublicKeys@2022-11-01"

resource_id = azapi_resource.ssh_public_key.id

action = "generateKeyPair"

method = "POST"

response_export_values = ["publicKey", "privateKey"]
}

resource "azapi_resource" "ssh_public_key" {

type = "Microsoft.Compute/sshPublicKeys@2022-11-01"

name = random_pet.ssh_key_name.id

location = azurerm_resource_group.main.location

parent_id = azurerm_resource_group.main.id

} 

output "key_data" {
value = jsondecode(azapi_resource_action.ssh_public_key_gen.output).publicKey
}

```


NOTA: usar una backend que ya exista y migrar el tfstate al nuevo
```provider.tf
terraform {

required_providers {

azurerm = {

source = "hashicorp/azurerm"

version = "~>3.2"

}

azapi = {

source = "azure/azapi"

version = "~>1.5"

}

random = {

source = "hashicorp/random"

version = "~>3.0"

}

time = {

source = "hashicorp/time"

version = "0.9.1"
}
}

backend "azurerm" {

resource_group_name = 
storage_account_name = 
container_name = 
key = 

subscription_id = 
tenant_id = 
client_id = 
client_secret = 

}

}

  

provider "azurerm" {

features {

key_vault {

purge_soft_delete_on_destroy = true

recover_soft_deleted_key_vaults = true

}

}
subscription_id = 
tenant_id = 
client_id = 
client_secret = 
}

```


Nota: usar terraform output -raw [poner le output]
```output.tf
output "resource_group_name" {

value = azurerm_resource_group.main.name

}

  

output "client_key" {

value = azurerm_kubernetes_cluster.main.kube_config.0.client_key

sensitive = true

}

  

output "client_certificate" {

value = azurerm_kubernetes_cluster.main.kube_config.0.client_certificate

sensitive = true

}

  

output "cluster_ca_certificate" {

value = azurerm_kubernetes_cluster.main.kube_config.0.cluster_ca_certificate

sensitive = true

}

  

output "cluster_username" {

value = azurerm_kubernetes_cluster.main.kube_config.0.username

sensitive = true

}

  

output "cluster_password" {

value = azurerm_kubernetes_cluster.main.kube_config.0.password

sensitive = true

}

  

output "kube_config" {

value = azurerm_kubernetes_cluster.main.kube_config_raw

sensitive = true

}

  

output "host" {

value = azurerm_kubernetes_cluster.main.kube_config.0.host

sensitive = true

}

  

output "identity_resource_id" {

value = azurerm_user_assigned_identity.main.id

}

  

output "identity_client_id" {

value = azurerm_user_assigned_identity.main.client_id

}

  

output "application_ip_address" {

value = azurerm_public_ip.main.ip_address

}
```

terraform init
terraform plan 
terraform apply

az aks update -g mmrv-staging-rg -n mmrv-staging-aks --enable-oidc-issuer --enable-workload-identity **IMPORTANTE: el oidc fue declarado en la infraestructura, pero el workload no, este comando puede ser innecesario**

export AKS_OIDC_ISSUER="$(az aks show -n mmrv-staging-aks -g mmrv-staging-rg --query "oidcIssuerProfile.issuerUrl" -otsv)" **nota : variable exportada para el comando de cread una entidad federal**

az keyvault secret set --vault-name mmrv-staging-kv --name “DATABASE-NAME” --value “mmrvbackend” **settea las variable de entorno de la base de datos en el vault**

az aks get-credentials -n mmrv-staging-aks -g mmrv-staging-rg

_az aks update -n_ mmrv-staging-aks _-g_ mmrv-staging-rg _--attach-acr mmrvstagingacr_  **pega la registri del kubernetes**

export USER_ASSIGNED_CLIENT_ID="$(az identity show --resource-group mmrv-staging-rg --name mmrv-staging-msi --query 'clientId' -otsv)"


##### crea una entidad federada
az identity federated-credential create --name ${FEDERATED_IDENTITY_CREDENTIAL_NAME} --identity-name ${USER_ASSIGNED_IDENTITY_NAME} --resource-group ${RESOURCE_GROUP} --issuer ${AKS_OIDC_ISSUER} --subject system:serviceaccount:${SERVICE_ACCOUNT_NAMESPACE}:${SERVICE_ACCOUNT_NAME}


az identity federated-credential create --name mmrv-staging-federated-msi --identity-name mmrv-staging-msi --resource-group mmrv-staging-rg --issuer ${AKS_OIDC_ISSUER} --subject system:serviceaccount:backend:mmrv-staging-msi-sa
the source : 'https://learn.microsoft.com/en-us/azure/aks/learn/tutorial-kubernetes-workload-identity'
#
##### te logueas en la registry de AWS

aws ecr get-login-password --region us-east-1 | docker login --username AWS --password-stdin 858332052541.dkr.ecr.us-east-1.amazonaws.com

docker pull [name imagen ]

aws sso logout
??? 'SSO_ACCOUNT=$(aws sts get-caller-identity --query "Account" --profile sso)'
docker logout
#

##### te logueas en la resgistry de AZURE
az acr login --name mmrvstagingacr (ubicar credenciales en el portal “access key”) 

docker tag [ imagen actual ]  [ imagen nueva ]

docker push [ imagen name ]
# comando kubectl

de aqui se empeezan a instalar los servicios 
como ingress-nginx

kubect apply -f [nombre del archivo] -n namespace

kubectl get pod -n namespace 

kubectl describe pod -n namespace podname

kubectl logs -n namespace podname