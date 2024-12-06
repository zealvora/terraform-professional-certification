
### Base Variable Code

```sh
variable "user_names" {
    type = list
    default = ["alice","bob","john"]
}

variable "ami" {
    type = map
    default  = {
        dev = "ami-123"
        stg = "ami-456"
        prd = "ami-789"
    }
}
```

### Example 1 - Using Simple For Expression to Verify Results
```sh
output "for_expression_list" {
    value = [for data in var.ami : upper(data)]
}
```

### Example 2 - Referencing to Key and Value from a Map

```sh
output "for_expression_list" {
    value = [for key,value in var.ami : upper(key)]
}
```
### Example 3 - Referencing to Index from a List

```sh
output "for_expression_list" {
    value = [for a,b in var.user_names : upper(a)]
}
```

### Example 4 - Using IF for filter elements

```sh
output "for_expression_list" {
    value = [for value in var.user_names : upper(value) if value == "alice"]
}
```

### Example 5 - Output Value with Different Data Type
```sh
output "for_expression_list" {
    value = {for value in var.user_names : value => upper(value)}
}
```