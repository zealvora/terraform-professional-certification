### Content of sg-04.csv file
```sh
name,direction,protocol,cidr_block,port
rule-01,in,tcp,app-1,80
rule-01,in,tcp,app-2,443
```

### Content of app.json file

```sh
{
    "app-1": "10.77.0.0/16",
    "app-2": "172.16.0.0/24"
}
```

### Solution - Part 1
```sh

locals {
    csv_data = csvdecode(file("./sg-04.csv"))
    json_data = jsondecode(file("./app.json"))

    processed_data = { for index, data in local.csv_data : index => {
        direction  = data.direction
        protocol   = data.protocol
        cidr_block = local.json_data[data.cidr_block]
        port       = data.port
    } }
}

output "this" {
    value = local.processed_data
}

resource "aws_security_group" "example" {
  name        = "usecase-04-sg"
}

resource "aws_vpc_security_group_ingress_rule" "example" {
  for_each = local.processed_data
  security_group_id = aws_security_group.example.id

  cidr_ipv4   = each.value.cidr_block
  from_port   = each.value.port
  ip_protocol = each.value.protocol
  to_port     = each.value.port
}
```

```sh
terraform apply -auto-approve
terraform destroy -auto-approve
```
### app-2.json (Used for Solution - Part 2)
```sh
{
    "app": "10.77.0.0/16",
    "database": "172.16.0.0/24"
}
```
### Solution - Part 2
```sh

locals {
    csv_data = csvdecode(file("./sg-04.csv"))
    json_data = jsondecode(file("./app-2.json"))

    processed_data = { for index, data in local.csv_data : index => {
        direction  = data.direction
        protocol   = data.protocol
        cidr_block = local.json_data[local.name_mapping[data.cidr_block]]
        port       = data.port
    } }

    name_mapping = {
        "app-1" = "app"
        "app-2" = "database"
    }
}

# local.json_data
#local.name_mapping[data.cidr_block] -> local.name_mapping["app-1"]
#local.json_data
#local.name_mapping["app-2"] --> database
#local.json_data["database"]
output "this" {
    value = local.json_data["database"]
}

resource "aws_security_group" "example" {
  name        = "usecase-04-sg"
}

resource "aws_vpc_security_group_ingress_rule" "example" {
  for_each = local.processed_data
  security_group_id = aws_security_group.example.id

  cidr_ipv4   = each.value.cidr_block
  from_port   = each.value.port
  ip_protocol = each.value.protocol
  to_port     = each.value.port
}
```

```sh
terraform apply -auto-approve
terraform destroy -auto-approve
```