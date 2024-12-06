
### Base Code Used (mysg.tf)

```sh
resource "aws_security_group" "this" {
  name        = "demo-firewall"
}

resource "aws_vpc_security_group_ingress_rule" "example" {
  security_group_id = aws_security_group.this.id

  cidr_ipv4   = "0.0.0.0/0"
  from_port   = 22
  ip_protocol = "tcp"
  to_port     = 22
}
```

### Command to Scan

```sh
checkov -f mysg.tf
checkov -f mysg.tf --check CKV_AWS_24

### Modified Code with Variable

```sh
resource "aws_security_group" "this" {
  name        = "demo-firewall"
}

variable "vpn_ip" {}
 
resource "aws_vpc_security_group_ingress_rule" "example" {
  security_group_id = aws_security_group.this.id

  cidr_ipv4   = var.vpn_ip
  from_port   = 22
  ip_protocol = "tcp"
  to_port     = 22
}
```
```sh
terraform plan -var="vpn_ip=0.0.0.0/0"
```

### Configuring PLAN Scans with Checkov

```sh
terraform plan --out tfplan.binary
terraform show -json tfplan.binary | jq > tfplan.json
checkov -f tfplan.json
```
```sh
checkov -f mysg.tf --check CKV_AWS_24
```

