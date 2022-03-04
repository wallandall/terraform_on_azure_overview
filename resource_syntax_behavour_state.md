# Terraform Resource Syntax, Behaviour and State
## Resource Syntax
Resource declarations can include a number of advanced features, but only a small subset are required for initial use.

```
resource "azurerm_resource_group" "myrg2" {
  nae = "myrg-2"
  location = "West Us"
  provider = azurerm.provider2-westus
  count = 2
}
```

A resource block declares a resource of a given type ("azurerm_resource_group") with a given local name ("myrg2"). The name is used to refer to this resource from elsewhere in the same Terraform module, but has no significance outside that module's scope.

The resource type and name together serve as an identifier for a given resource and so must be unique within a module.

Within the block body (between { and }) are the configuration arguments for the resource itself. Most arguments in this section depend on the resource type, and indeed in this example both ami and instance_type are arguments defined specifically for the aws_instance resource type.

Each resource is associated with a single resource type, which determines the kind of infrastructure object it manages and what arguments and other attributes the resource supports.

## Resource  Behavior
A resource block declares that you want a particular infrastructure object to exist with the given settings. If you are writing a new configuration for the first time, the resources it defines will exist only in the configuration, and will not yet represent real infrastructure objects in the target platform.

Applying a Terraform configuration is the process of creating, updating, and destroying real infrastructure objects in order to make their settings match the configuration.

When Terraform creates a new infrastructure object represented by a resource block, the identifier for that real object is saved in Terraform's state, allowing it to be updated and destroyed in response to future changes. For resource blocks that already have an associated infrastructure object in the state, Terraform compares the actual configuration of the object with the arguments given in the configuration and, if necessary, updates the object to match the configuration.

In summary, applying a Terraform configuration will:

* Create resources that exist in the configuration but are not associated with a real infrastructure object in the state.
* Destroy resources that exist in the state but no longer exist in the configuration.
* Update in-place resources whose arguments have changed.
* Destroy and re-create resources whose arguments have changed but which cannot be updated in-place due to remote API limitations.
  
This general behavior applies for all resources, regardless of type. The details of what it means to create, update, or destroy a resource are different for each resource type, but this standard set of verbs is common across them all.

## Terraform State
Terraform must store state about your managed infrastructure and configuration. This state is used by Terraform to map real world resources to your configuration, keep track of metadata, and to improve performance for large infrastructures.

This state is stored by default in a local file named "terraform.tfstate", but it can also be stored remotely, which works better in a team environment.

Terraform uses this local state to create plans and make changes to your infrastructure. Prior to any operation, Terraform does a refresh to update the state with the real infrastructure.

The primary purpose of Terraform state is to store bindings between objects in a remote system and resource instances declared in your configuration. When Terraform creates a remote object in response to a change of configuration, it will record the identity of that remote object against a particular resource instance, and then potentially update or delete that object in response to future configuration changes.
