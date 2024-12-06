### Base JSON Used (config.json)

```sh
{
    "servers": [
      {
        "name": "web01",
        "ip": "192.168.1.1",
        "roles": ["web", "app"],
        "metadata": {
          "owner": "teamA",
          "environment": "production",
          "dns": ["1.1.1.1"]
        }
      },
      {
        "name": "web02",
        "ip": "192.168.1.2",
        "roles": ["web"],
        "metadata": {
          "owner": "teamB",
          "environment": "development"
        }
      },
      {
        "name": "db01",
        "ip": "192.168.1.10",
        "roles": ["db"],
        "metadata": {
          "owner": "teamA",
          "environment": "production"
        }
      }
    ],
    "network": {
      "subnets": ["192.168.1.0/24", "192.168.2.0/24"],
      "dns": ["8.8.8.8", "8.8.4.4"]
    },
    "features": {
      "monitoring": true,
      "logging": false,
      "alerting": true,
      "security": true
    }
  }
```

### Base Terraform Code Used

```sh
locals {
  config = jsondecode(file("${path.module}/config.json"))
}
```

### Use-Case 1 Code
```sh
output "usecase01" {
  value = [ for data in local.config : data]
}
```

### Use-Case 2 Code
```sh
output usecase02 {
  value = [ for data in local.config.servers : data.name ]
}
```

### Use-Case 3 Code
```sh
output usecase03 {
  value = { for data in local.config.servers : data.name => data.ip }
}
```

### Use-Case 4 Code
```sh
output usecase04 {
  value = [ for data in local.config.servers : data.ip if data.metadata.environment == "production"]
}
```

### Use-Case 5 Code
```sh
output usecase05 {
  value = distinct(flatten([ for data in local.config.servers : data.roles ]))
}

```

### Use-Case 6 Code
```sh
output usecase06 {
  value = [ for data in local.config.servers : "${data.name} (${data.metadata.environment})"]
}
```

### Use-Case 7 Code
```sh
output usecase07 {
  value = [ for data in local.config.servers : "${data.ip} roles: ${join(",",data.roles)}"]
}
```

