# Terraform Dependency Lock File

A Terraform configuration may refer to two different kinds of external dependency that come from outside of its own codebase:

* Providers, which are plugins for Terraform that extend it with support for interacting with various external systems.
* Modules, which allow splitting out groups of Terraform configuration constructs (written in the Terraform language) into reusable abstractions.

Both of these dependency types can be published and updated independently from Terraform itself and from the configurations that depend on them. For that reason, Terraform must determine which versions of those dependencies are potentially compatible with the current configuration and which versions are currently selected for use.

Version constraints within the configuration itself determine which versions of dependencies are potentially compatible, but after selecting a specific version of each dependency Terraform remembers the decisions it made in a dependency lock file so that it can (by default) make the same decisions again in future.

At present, the dependency lock file tracks only provider dependencies. Terraform does not remember version selections for remote modules, and so Terraform will always select the newest available module version that meets the specified version constraints. You can use an exact version constraint to ensure that Terraform will always select the same module version.

## Lock File Location
The dependency lock file is a file that belongs to the configuration as a whole, rather than to each separate module in the configuration. For that reason Terraform creates it and expects to find it in your current working directory when you run Terraform, which is also the directory containing the .tf files for the root module of your configuration.

The lock file is always named .terraform.lock.hcl, and this name is intended to signify that it is a lock file for various items that Terraform caches in the .terraform subdirectory of your working directory.

Terraform automatically creates or updates the dependency lock file each time you run the terraform init command. You should include this file in ___your version control___ repository so that you can discuss potential changes to your external dependencies via code review, just as you would discuss potential changes to your configuration itself.

The dependency lock file uses the same low-level syntax as the main Terraform language, but the dependency lock file is not itself a Terraform language configuration file. It is named with the suffix .hcl instead of .tf in order to signify that difference.