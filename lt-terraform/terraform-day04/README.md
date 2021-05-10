# Conditions

An operator is a type of expression that transforms or combines one or more other expressions. Operators either combine two values in some way to produce a third result value, or transform a single given value to produce a single result.

Operators that work on two values place an operator symbol between the two values, similar to mathematical notation: 1 + 2. Operators that work on only one value place an operator symbol before that value, like !true.

The Terraform language has a set of operators for both arithmetic and logic, which are similar to operators in programming languages such as JavaScript or Ruby.

## Notes

* Extra Reading:
  * https://www.terraform.io/docs/configuration/expressions.html#arithmetic-and-logical-operators
* Example usage:
  * count = var.environment == "production" ? 2 + var.extra : 1
* count.index can be something to help you provide different resources based on the "count" parameter

---

# Type Constraints

Terraform module authors and provider developers can use detailed type constraints to validate user-provided values for their input variables and resource arguments. This requires some additional knowledge about Terraform's type system, but allows you to build a more resilient user interface for your modules and resources.

## Notes

* Extra reading:
  * https://www.terraform.io/docs/configuration/types.html

---

# Loop for_each

By default, a resource block configures one real infrastructure object. (Similarly, a module block includes a child module's contents into the configuration one time.) However, sometimes you want to manage several similar objects (like a fixed pool of compute instances) without writing a separate block for each one. Terraform has two ways to do this: count and for_each.

If a resource or module block includes a for_each argument whose value is a map or a set of strings, Terraform will create one instance for each member of that map or set.

## Notes

* Extra reading:
  * https://www.terraform.io/docs/configuration/meta-arguments/for_each.html

