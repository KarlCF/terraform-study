# Dynamic Blocks

Within top-level block constructs like resources, expressions can usually be used only when assigning a value to an argument. This covers many uses, but some resource types include repeatable nested blocks in their arguments, which do not accept expressions.

You can dynamically construct repeatable nested blocks like setting using a special dynamic block type, which is supported inside resource, data, provider, and provisioner blocks.

## Notes

* Extra reading:
  * https://www.terraform.io/docs/configuration/expressions/dynamic-blocks.html

---

# String Template

Within quoted and heredoc string expressions, the sequences ${ and %{ begin template sequences. Templates let you directly embed expressions into a string literal, to dynamically construct strings from other values.

## Notes

* Extra Reading:
  * https://www.terraform.io/docs/configuration/expressions/strings.html

---

# Terraform Cloud

When run locally, Terraform manages each collection of infrastructure with a persistent working directory, which contains a configuration, state data, and variables. Since Terraform CLI uses content from the directory it runs in, you can organize infrastructure resources into meaningful groups by keeping their configurations in separate directories.

Terraform Cloud manages infrastructure collections with workspaces instead of directories. A workspace contains everything Terraform needs to manage a given collection of infrastructure, and separate workspaces function like completely separate working directories.

Note: Terraform Cloud and Terraform CLI both have features called "workspaces," but they're slightly different. CLI workspaces are alternate state files in the same working directory; they're a convenience feature for using one configuration to manage multiple similar groups of resources.
## Notes

* Extra Reading:
  * https://www.terraform.io/docs/cloud/workspaces/index.html
