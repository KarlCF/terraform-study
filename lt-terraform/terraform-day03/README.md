# Getting Help

While it's important to have the previous knowledge to execute your tasks, it's very common that you will find new and different challenges along the way. That being said, it's important also to know where to find the answers to your problems.

## Notes

* The suffix -h on any command will return some info regarding the command that you need to know more about
* It's best to try to find things out by yourself before looking up online

---

# Dependencies

Most of the time, Terraform infers dependencies between resources based on the configuration given, so that resources are created and destroyed in the correct order. Occasionally, however, Terraform cannot infer dependencies between different parts of your infrastructure, and you will need to create an explicit dependency with the depends_on argument.

Terraform version 0.13 added the ability to create explicit dependencies between modules and resources. Prior versions only allowed explicit dependencies on resources.

## Notes

* https://learn.hashicorp.com/tutorials/terraform/dependencies

---

# Terraform Commands & Verbose

Terraform has detailed logs which can be enabled by setting the TF_LOG environment variable to any value. This will cause detailed logs to appear on stderr.

You can set TF_LOG to one of the log levels TRACE, DEBUG, INFO, WARN or ERROR to change the verbosity of the logs. TRACE is the most verbose and it is the default if TF_LOG is set to something other than a log level name.

To persist logged output you can set TF_LOG_PATH in order to force the log to always be appended to a specific file when logging is enabled. Note that even when TF_LOG_PATH is set, TF_LOG must be set in order for any logging to be enabled.

If you find a bug with Terraform, please include the detailed log by using a service such as gist.

## Notes

* Extra Reading:
  * https://www.terraform.io/docs/internals/debugging.html

---

# Taint

The terraform taint command manually marks a Terraform-managed resource as tainted, forcing it to be destroyed and recreated on the next apply.

This command will not modify infrastructure, but does modify the state file in order to mark a resource as tainted. Once a resource is marked as tainted, the next plan will show that the resource will be destroyed and recreated and the next apply will implement this change.

## Notes

* Extra reading:
  * https://www.terraform.io/docs/commands/taint.html

---

# Graph

The terraform graph command is used to generate a visual representation of either a configuration or execution plan. The output is in the DOT format, which can be used by GraphViz to generate charts.

## Notes

* Extra Reading:
  * https://www.terraform.io/docs/commands/graph.html
* Extra Content:
  * https://www.youtube.com/watch?v=Frmwdter-vQ&feature=youtu.be [Portuguese]
* The output of terraform graph is in the DOT format, which can easily be converted to an image by making use of dot provided by GraphViz:

```terraform graph | dot -Tsvg > graph.svg```

--- 

# fmt

The terraform fmt command is used to rewrite Terraform configuration files to a canonical format and style. This command applies a subset of the Terraform language style conventions, along with other minor adjustments for readability.

Other Terraform commands that generate Terraform configuration will produce configuration files that conform to the style imposed by terraform fmt, so using this style in your own files will ensure consistency.

The canonical format may change in minor ways between Terraform versions, so after upgrading Terraform we recommend to proactively run terraform fmt on your modules along with any other changes you are making to adopt the new version.

## Notes

* Extra reading:
  * https://www.terraform.io/docs/commands/fmt.html
  * https://www.terraform.io/docs/configuration/style.html

--- 

# validate

The terraform validate command validates the configuration files in a directory, referring only to the configuration and not accessing any remote services such as remote state, provider APIs, etc.

Validate runs checks that verify whether a configuration is syntactically valid and internally consistent, regardless of any provided variables or existing state. It is thus primarily useful for general verification of reusable modules, including correctness of attribute names and value types.

## Notes

* Very usefull for running on CI
* Extra reading:
  * https://www.terraform.io/docs/commands/validate.html