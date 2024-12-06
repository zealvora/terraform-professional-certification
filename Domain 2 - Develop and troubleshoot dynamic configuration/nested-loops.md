
### Example Code 1

```sh
variable "list_01" {
    type = list
    default = [1,2,3]
}

variable "list_02" {
    type = list
    default = [4,5,6]
}

output "this" {
    value = [ for data in var.list_01 : [ for value in var.list_02 : "${data} ${value}" ] ]
}
```

### Example Code 2

```sh
locals {
    x = range(3)
    y = range(1,10)
}

output "list_of_lists" {
  value = distinct(flatten([for x in local.x : [for y in local.y : y]]))
}
```