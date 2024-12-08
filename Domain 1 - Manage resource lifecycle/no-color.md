
### Base Code Used

```sh
resource "aws_security_group" "firewall" {
  name        = "kplabs"
}
```

### Command Used
```sh
terraform plan
terraform plan -no-color
terraform apply -auto-approve
```

```sh
terraform plan > color.plan
terraform plan -no-color > nocolor.plan
```