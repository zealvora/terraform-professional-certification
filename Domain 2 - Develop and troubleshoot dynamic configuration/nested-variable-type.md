
### Example 1 - List of Lists
```sh
variable "list_of_list" {
    type = list(list(string))
    default = [["alice","james"],["bob"],["john"]]
}

output "list_of_lists" {
    value = var.list_of_list
}
```

### Example 2 - List of Maps
```sh
variable "list_of_maps" {
    type = list(map(string))
    default = [
        {
            user = "alice"
            email = "alice@kplabs.in"
        },
        {
            user = "bob"
            email = "bob@kplabs.in"
        }
        ]
}

output "list_of_maps" {
    value = var.list_of_maps
}
```

### Example 3 - Map of Maps
```sh
variable "map_of_maps" {
    type = map(map(string))
    default = {
        dev = {
            instance_type = "t2.micro"
            Name          = "dev-server"
        },
        prod = {
            instance_type = "m5.large"
            Name          = "prod-server"
        }
    }
}

output "map_of_maps" {
    value = var.map_of_maps
}
```

### Example 4 - Map of Lists
```sh
variable "map_of_lists" {
    type = map(list(string))
    default = {
       name=["alice"],
       names=["bob"]
    }
}

output "map_of_lists" {
    value = var.map_of_lists
}
```

### Example 5 - List of Objects
```sh
variable "list_of_objects" {
    type = list(object({
        name = string
        age  = number
        tags = map(string)
    }))
    default = [
        {
            name = "alice"
            age  =  32
            tags = {"env"="dev","name"="alice"}
        }
    ]
}

output "list_of_objects" {
    value = var.list_of_objects
}
```

