# Terraform Settings and Provider Block

Terraform Settings Block is a special block used to configure behaviour such as :
* The required Terraform CLI Version
* The Provider Requirements and Version
* The Terraform Backend which is used to store the Terraform State in a remote location. If no defined, the Terraform State file will be stored locally.

The Provider Block is where you define the provider that Terraform will communicate with i.e Azure, Google, AWS etc 

Resource Block is a standard block where you define your resources.