## Terraform Basic Commands

The below table displays the 5 basic Terraform commands and where they are run withing the Terraform Workflow

|                                              Step 1: Init                                              |                                                                Step 2: Validate                                                                |                                                               Step 3: Plan                                                               |                                                      Step 4: Apply                                                      | Step 5: Destroy                                                                     |
| :----------------------------------------------------------------------------------------------------: | :--------------------------------------------------------------------------------------------------------------------------------------------: | :--------------------------------------------------------------------------------------------------------------------------------------: | :---------------------------------------------------------------------------------------------------------------------: | ----------------------------------------------------------------------------------- |
|                                           ``terraform init``                                           |                                                             ``terraform validate``                                                             |                                                            ``terraform plan``                                                            |                                                   ``terrafom apply``                                                   | ``terraform destroy``                                                               |
|                Used to initialise a working directory containing terraform config files                | Validates the terraform configuration files in the respective directory to ensure that they are syntactically valid and internally consistent. |                                                        Creates an execution plan                                                        |                   Used to apply the changes required to reach the desired state of the configuration.                   | Used to destroy the Terraform managed infrastructure                                |
| ``terraform init`` is the first command that should be run after writing a new Terraform configuration |                                                                                                                                               | Terraform performs a refresh and determines what actions are necessary to achieve the desired state specified in the configuration files | By default,``terraform apply`` scans the current directory for the configuration and applies the changes appropriately. | Running ``terraform destoy`` will ask for confirmation before destroying resources. |
|                   Downloads [Providers](https://registry.terraform.io/browse/providers)                   |                                                                                                                                               |                                                                                                                                         |                                                                                                                         |                                                                                     |


Before running Terraform Commands, you need to be logged into your Azure Tenant, have a region set as well as specify your Subscription ID. This can be achieved by the following commands

* Log into Azure ```az login```
* List all [Azure Regions](https://docs.microsoft.com/en-us/azure/virtual-machines/regions) in  a Table : ```az account list-locations -o table```
* Set a Specific Subscription ```az account set --subscription="Subscription_id"```

The below code defines the Terraform Configuration file for the Azure Provider, additional provider can be found [here](https://registry.terraform.io/browse/providers)


```
terraform {
  required_providers {
    azurerm = {
      source = "hashicorp/azurerm"
      version = "2.98.0"
    }
  }
}
# Configure the Microsoft Azure Provider
provider "azurerm" {
  features {}
}
# Create Resource Group 
resource "azurerm_resource_group" "my_demo_rg1" {
  location = "germanynorth"
  name = "demo-rg1"  
}
```
1. Save the configuration and run ```terraform init``` from the same directory as the file. When you run ```terraform init``` the following will happen:
   1. This will initialise terraform by downloading the specified version of the provider
   2. Terraform will create a lockfile called ___.terraform.lock.hcl___ which is used to record the provider selection that was initialised.This file shoiuld be included in your version control
   
2. ```terraform validate``` will validate the files in the current directoy
3. ```terraform plan``` generates the plan of the resources that will be created in Azure. 
4. ```terraform apply```  will ask you to confirm the creation of the resouces in Azure. Once confirmed the resources will be created. Additionally ___terraform.tfstate___ file will be created which tracks changes that have been deployed to Azure
5. To delete the resources created by terraform, run ```terraform destroy```

[Back to Index](ReadMe.md)
