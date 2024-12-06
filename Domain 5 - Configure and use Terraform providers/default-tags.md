
### Base Code
```sh
resource "aws_security_group" "allow_tls" {
  name        = "demo-firewall"
}

resource "aws_iam_user" "this" {
  name = "kplabs-user"
}
```
### Code with Default Tags
```sh
provider "aws" {
  default_tags {
   tags = {
     Team    = "Security"
     Managed = "Terraform"
     Env     = "Production"
  }
  }
}

resource "aws_security_group" "allow_tls" {
  name        = "demo-firewall"
}

resource "aws_iam_user" "this" {
  name = "kplabs-user"
}
```

### Overriding Default Tags
```sh
resource "aws_security_group" "allow_tls" {
  name        = "demo-firewall"

  tags = {
    Team = "Networking"
  }
}

resource "aws_iam_user" "this" {
  name = "kplabs-user"
}
```


