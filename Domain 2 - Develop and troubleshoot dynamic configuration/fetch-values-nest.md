
### Example 1 - Fetching Values from List
```sh
variable "demo_lists" {
  type = list
  default = ["apple","banana","mango","grapes"]
}

output "list_values" {
  value = length(var.demo_lists)
}
```

### Example 2 - Fetching Values from List of Lists
```sh
variable "matrix_config" {
  type = list(list(string))
  default = [
    ["a1", "a2", "a3"],
    ["b1", "b2", "b3"],
    ["c1", "c2"]
  ]
}

output "list_values" {
  value = length(var.matrix_config)
}
```

### Example 3 - Fetching Values from List of Lists
```sh
variable "matrix_config" {
  type = list(list(string))
  default = [
    ["a1", "a2", "a3"],
    ["b1", "b2", "b3"],
    [],
    ["c1", "c2"]
  ]
}
output "matrix_config" {
    value = var.matrix_config[1][1]
}
```


### Example 4 - Fetching Values from List of Map
```sh
variable "users" {
  type = list(map(string))
  default = [
    {
      name  = "john"
      role  = "admin"
      email = "john@example.com"
    },
    {
      name  = "jane"
      role  = "developer"
      email = "jane@example.com"
    }
  ]
}

output "first_user_name" {
  value = var.users[0]["email"]
}
```


### Example 5 - Fetching Values from Map of Map
```sh
variable "environment_config" {
  type = map(map(string))
  default = {
    dev = {
      instance_type = "t2.micro"
      region        = "us-east-1"
      replicas      = "1"
    }
    prod = {
      instance_type = "t2.large"
      region        = "us-west-2"
      replicas      = "3"
    }
  }
}

output "dev_instance_type" {
  value = var.environment_config["dev"]["instance_type"]
}
```

### Example 6 - Fetching Values from List of Object
```sh
variable "instances" {
  type = list(object({
    name          = string
    instance_type = string
    tags          = map(string)
  }))
  default = [
    {
      name          = "web-server"
      instance_type = "t2.micro"
      tags          = { "env" = "production", "role" = "web" }
    },
    {
      name          = "db-server"
      instance_type = "t2.medium"
      tags          = { "env" = "production", "role" = "db" }
    }
  ]
}

output "instances" {
  value = var.instances[0]["tags"]["env"]
}
```