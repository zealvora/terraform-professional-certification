
### Documentation Referenced

https://registry.terraform.io/providers/hashicorp/aws/latest/docs#assuming-an-iam-role

https://docs.aws.amazon.com/IAM/latest/UserGuide/id_roles_use_permissions-to-switch.html

### Base Code

```sh
resource "aws_security_group" "allow_tls" {
  name        = "demo-firewall"
}
```
### Base IAM Assume Role Policy

```sh
{
  "Version": "2012-10-17",
  "Statement": {
    "Effect": "Allow",
    "Action": "sts:AssumeRole",
    "Resource": "arn:aws:iam::account-id:role/Test*"
  }
}
```
### Final Code

```sh
provider "aws" {
  assume_role {
    role_arn     = "arn:aws:iam::042025557788:role/TerraformAssumeRole"
    session_name = "kplabs-session"
  }
}

resource "aws_security_group" "allow_tls" {
  name        = "demo-firewall"
}
```