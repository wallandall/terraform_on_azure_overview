# Terraform Language Basics
* Terraform code is stored in plain text files with the ___.tf___ file extension
* Terraform files can also be stored in ___tf.json___ files which uses a JSON notation but this is not as common as ___.tf___ files. 
* Terraform uses HCL which is the HashiCorp Language and includes:
  * Blocks are containers for other content and usually represent the configuration of some kind of object, like a resource. Blocks have a block type, can have zero or more labels, and have a body that contains any number of arguments and nested blocks. Most of Terraform's features are controlled by top-level blocks in a configuration file.
  * Arguments assign a value to a name. They appear within blocks.
  * Expressions represent a value, either literally or by referencing and combining other values. They appear as values for arguments, or within other expressions.
  * Comments can be used by using either ``` # ``` ot multiline comments ``` */.....*/ ```
  * The Terraform language is declarative, describing an intended goal rather than the steps to reach that goal. The ordering of blocks and the files they are organized into are generally not significant; Terraform only considers implicit and explicit relationships between resources when determining an order of operations.