
### Contents of sg-03.csv file

```sh
name,direction,protocol,cidr_block,port
rule-01,in,tcp,172.31.0.0/16,443-445
rule-01,in,tcp,196.18.10.50/32,80-100
rule-01,in,tcp,10.77.0.35/32,8443
```


### Final Solution (use-case-03.tf)

```sh
locals {
  csv_data = csvdecode(file("./sg-03.csv"))

  processed_data = [ for data in local.csv_data : {
    name = data.name
    direction = data.direction
    protocol = data.protocol
    cidr_block = data.cidr_block
    from_port = can(regex("-",data.port)) ? split("-",data.port)[0] : data.port
    to_port   = can(regex("-",data.port)) ? split("-",data.port)[1] : data.port
  }]

  for_each = { for index, data in local.processed_data : index => data } 
}
/*
output "this" {
    value = local.for_each
}
*/
resource "aws_security_group" "example" {
  name        = "usecase-03-sg"
}

resource "aws_vpc_security_group_ingress_rule" "example" {
  for_each = { for index, data in local.processed_data : index => data } 
  security_group_id = aws_security_group.example.id

  cidr_ipv4   = each.value.cidr_block
  from_port   = each.value.from_port
  ip_protocol = each.value.protocol
  to_port     = each.value.to_port
}
```