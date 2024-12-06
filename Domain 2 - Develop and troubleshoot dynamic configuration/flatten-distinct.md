
### Base Code

```sh
locals {
  instance_configs = [
    {
      name = "web"
      tags = ["http", "https", "web"]
    },
    {
      name = "app"
      tags = ["application", "backend","http", "https"]
    }
  ]
}
```

### Final Output Values

```sh
output "this" {
  value = distinct(flatten([ for data in local.instance_configs : data.tags ]))
}
```