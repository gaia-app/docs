# Gaia concepts

## Module

> A module is a container for multiple resources that are used together. Modules can be used to create lightweight abstractions, so that you can describe your infrastructure in terms of its architecture, rather than directly in terms of physical objects.
> 
> [Terraform documentation](https://www.terraform.io/docs/modules/index.html)

Gaia modules translates exactly to Terraform modules.

Gaia modules can be created manually from a simple URL, or can be imported from Github or Gitlab when using OAuth2 authentication and Registries integration.

## Stack

A stack is the instanciation of a Gaia module, using variables and credentials.
It has its own lifecycle.

It can be roughly compared to Terraform workspaces.

Instanciation of cloud resources, using terraform scripts is done by the Jobs.

Thus, a stack can be created in Gaia, without having to really instanciate all the ressources a `terraform apply` could create.

## Job

A job is either : 

 * the instanciation of a stack (`terraform plan` > `terraform apply`)
 * the update of a stack (`terraform plan` > `terraform apply`)
 * the deleting of a stack (`terraform plan --destroy` > `terraform destroy`)

A stack can thus be destroyed at some time, Gaia will save the variables to use them if the stack needs to be re-created at some time.

## Step

A step is the smallest execution that Gaia can manage.
Depending on the Job type, it can be:

* terraform plan
* terraform apply
* terraform plan --destroy
* terraform destroy

Each step is run in isolation.

## Credentials

Gaia supports credentials management by allowing administrators to store credentials, and make them usable by Gaia users in their stacks.
Credentials can take multiple forms, depending on the target Terraform provider that will be used in the Module and in the Stack

* access keys for AWS & Azure modules
* service account JSON for GCP modules

When using Vault integration, Gaia securely encrypts the credentials before storing them in the database, using a `Transit` engine.
Gaia can also use `AWS` secret engine to dynamically generate AWS access credentials.
