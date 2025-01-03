
### Contents of sg-02.csv file

```sh
name,direction,protocol,cidr_block,port
rule-01,in,tcp,172.31.0.0/16,443
rule-01,in,tcp,172.31.0.0/16,80
rule-02,out,tcp,10.66.0.0/16,8443
rule-02,out,tcp,10.77.0.0/16,3306
```

### Final Solution (use-case-02.tf)

```sh

locals {
    csv_data = csvdecode(file("./sg-02.csv"))
    inbound_rules = [ for rule in local.csv_data : rule if rule.direction == "in"]
    outbound_rules = [ for rule in local.csv_data : rule if rule.direction == "out"]
    for_each = { for index, data in local.inbound_rules : index => data }
}
/*
output "csv" {
    value = local.for_each
}
*/
resource "aws_security_group" "example" {
  name        = "usecase-02-sg"
}

resource "aws_vpc_security_group_ingress_rule" "example" {
  for_each = { for index, data in local.inbound_rules : index => data }
  security_group_id = aws_security_group.example.id

  cidr_ipv4   = each.value.cidr_block
  from_port   = each.value.port
  ip_protocol = each.value.protocol
  to_port     = each.value.port
}

resource "aws_vpc_security_group_egress_rule" "example" {
  for_each = { for index, data in local.inbound_rules : index => data }
  security_group_id = aws_security_group.example.id

  cidr_ipv4   = each.value.cidr_block
  from_port   = each.value.port
  ip_protocol = each.value.protocol
  to_port     = each.value.port
}
```