### AWS Provider Documentation

https://registry.terraform.io/providers/hashicorp/aws/latest/docs

### Code Used:

```sh
provider "aws" {
  shared_config_files = ["C:/kplabs-aws-creds/config"]
  shared_credentials_files = ["C:/kplabs-aws-creds/credentials"]
}

resource "aws_security_group" "allow_tls" {
  name        = "demo-firewall"
}
```