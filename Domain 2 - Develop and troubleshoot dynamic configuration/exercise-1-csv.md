
### Contents of sg-01.csv file

```sh
name,direction,protocol,cidr_block,port
rule-01,in,tcp,172.31.0.0/16,443
rule-02,in,tcp,172.31.0.0/16,80
rule-03,out,tcp,10.66.0.0/16,8443
rule-04,out,tcp,10.77.0.0/16,3306
```

### Final Solution Code (use-case-01.tf)

```sh
locals {
    csv_data = csvdecode(file("./sg-01.csv"))
    inbound_rules = [ for rule in local.csv_data : rule if rule.direction == "in"]
    outbound_rules = [ for rule in local.csv_data : rule if rule.direction == "out"]
    for_each = { for data in local.inbound_rules : data.name => data}
}
/*
output "csv" {
    value = local.for_each
}
*/
resource "aws_security_group" "example" {
  name        = "usecase-01-sg"
}

resource "aws_vpc_security_group_ingress_rule" "example" {
  for_each = { for data in local.inbound_rules : data.name => data }
  security_group_id = aws_security_group.example.id

  cidr_ipv4   = each.value.cidr_block
  from_port   = each.value.port
  ip_protocol = each.value.protocol
  to_port     = each.value.port
}

resource "aws_vpc_security_group_egress_rule" "example" {
  for_each = { for data in local.outbound_rules : data.name => data }
  security_group_id = aws_security_group.example.id

  cidr_ipv4   = each.value.cidr_block
  from_port   = each.value.port
  ip_protocol = each.value.protocol
  to_port     = each.value.port
}
```