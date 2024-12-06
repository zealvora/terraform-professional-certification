
### Code Used (jsondecode-examples.tf)

#### Example 1 - Filtering Value based on Keys
```sh
locals {
  json_string = <<EOT
  {
    "name": "Mr A",
    "age": 30,
    "city": "Mumbai"
  }
  EOT

  decoded_json = jsondecode(local.json_string)
}

output "decode" {
    value = local.decoded_json["name"]
}
```
```sh
terraform apply -auto-approve
```
#### Example 2 - Array of Strings
```sh
locals {
  json_string = <<EOT
  [
    "apple",
    "banana",
    "cherry"
  ]
  EOT

  decoded_json = jsondecode(local.json_string)
}

output "decode" {
    value = local.decoded_json[0]
}
```
```sh
terraform apply -auto-approve
```
#### Example 3 - Array of Objects (Reference by Index)

```sh
locals {
  json_string = <<EOT
  [
    { "name": "Alice", "age": 25 },
    { "name": "Bob", "age": 28 },
    { "name": "Charlie", "age": 35 }
  ]
  EOT

  decoded_json = jsondecode(local.json_string)
}

output "decode" {
    value = local.decoded_json[0]
}
```
```sh
terraform apply -auto-approve
```

#### Example 4 - Array of Objects (Reference by Index and Name)

```sh
locals {
  json_string = <<EOT
  [
    { "name": "Alice", "age": 25 },
    { "name": "Bob", "age": 28 },
    { "name": "Charlie", "age": 35 }
  ]
  EOT

  decoded_json = jsondecode(local.json_string)
}

output "decode" {
    value = local.decoded_json[0]["name"]
}
```
```sh
terraform apply -auto-approve
```