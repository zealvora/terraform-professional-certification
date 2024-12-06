### for.tf

```sh
variable "user_names" {
    type = list
    default = ["alice","bob","john"]
}

output "for_expression" {
    value = [for zeal in var.user_names : upper(zeal)]
}
```

```sh
terraform console
upper("alice")
```