# Modules

A module is a container for multiple resources that are used together. Modules can be used to create lightweight abstractions, so that you can describe your infrastructure in terms of its architecture, rather than directly in terms of physical objects.

## Notes

* Best to leave your provider & terraform (backend) info on the main.tf file on the root of the project
* Important to remember:
  * If you need to output your child module data, it needs to be output to the root module, and then configured again
* Extra reading:
  * https://www.terraform.io/docs/configuration/modules.html

--- 

# Backend

A "backend" in Terraform determines how state is loaded and how an operation such as apply is executed. This abstraction enables non-local file state storage, remote execution, etc.

By default, Terraform uses the "local" backend, which is the normal behavior of Terraform you're used to.

## Notes

* Terraform detects changes on the state configuration and helps you transition this change
* Terraform must initialize any configured backend before use. This can be done by simply running terraform init.
* Backends are responsible for storing state and providing an API for state locking. State locking is optional. Despite the state being stored remotely, all Terraform commands such as terraform console, the terraform state operations, terraform taint, and more will continue to work as if the state was local.
* State Locking is highly reccomended while working as a team
* Extra reading:
  * https://www.terraform.io/docs/backends/index.html
  * https://www.terraform.io/docs/configuration/backend.html
  * https://www.terraform.io/docs/backends/config.html
  * https://www.terraform.io/docs/backends/init.html
  * https://www.terraform.io/docs/backends/state.html

---

# State

Terraform must store state about your managed infrastructure and configuration. This state is used by Terraform to map real world resources to your configuration, keep track of metadata, and to improve performance for large infrastructures.

## Notes

* Review:
  * terraform state pull
  * terraform state push
* Check out tool: jq
* Extra Reading:
  * https://www.terraform.io/docs/state/index.html
  * https://www.terraform.io/docs/state/purpose.html
  * https://www.terraform.io/docs/commands/state/index.html

## State Command

The terraform state command is used for advanced state management. As your Terraform usage becomes more advanced, there are some cases where you may need to modify the Terraform state. Rather than modify the state directly, the terraform state commands can be used in many cases instead.

# Import

Terraform is able to import existing infrastructure. This allows you take resources you've created by some other means and bring it under Terraform management.

This is a great way to slowly transition infrastructure to Terraform, or to be able to be confident that you can use Terraform in the future if it potentially doesn't support every feature you need today.

## Notes

* Check the docs of each resource in order to know the appropriate way to import them
* Extra Reading:
  * https://www.terraform.io/docs/import/index.html

---

# Workspace

Each Terraform configuration has an associated backend that defines how operations are executed and where persistent data such as the Terraform state are stored.

The persistent data stored in the backend belongs to a workspace. Initially the backend has only one workspace, called "default", and thus there is only one Terraform state associated with that configuration.

Certain backends support multiple named workspaces, allowing multiple states to be associated with a single configuration. The configuration still has only one backend, but multiple distinct instances of that configuration to be deployed without configuring a new backend or changing authentication credentials.

Terraform starts with a single workspace named "default". This workspace is special both because it is the default and also because it cannot ever be deleted. If you've never explicitly used workspaces, then you've only ever worked on the "default" workspace.

Workspaces are managed with the terraform workspace set of commands. To create a new workspace and switch to it, you can use terraform workspace new; to switch workspaces you can use terraform workspace select; etc.

## Notes

* Using conditionals, you can simply switch workspaces and deploy your infrastructure with different profiles/accounts/regions
* Extra Reading:
  * https://www.terraform.io/docs/state/workspaces.html

---

# Sensitive Data in State

Terraform state can contain sensitive data, depending on the resources in use and your definition of "sensitive." The state contains resource IDs and all resource attributes. For resources such as databases, this may contain initial passwords.

When using local state, state is stored in plain-text JSON files.

When using remote state, state is only ever held in memory when used by Terraform. It may be encrypted at rest, but this depends on the specific remote state backend.

## Notes

* Even though the backend is configured remotely, always encrypt the data if possible
* Extra reading:
  * https://www.terraform.io/docs/state/sensitive-data.html
  * https://www.terraform.io/docs/backends/types/s3.html