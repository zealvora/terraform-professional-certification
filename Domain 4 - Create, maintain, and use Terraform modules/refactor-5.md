
### Base Code Used
```sh
resource "aws_iam_user" "lb" {
  name = "alice-user"
}

resource "aws_security_group" "sg" {
  name        = "demo-sg"
}
```

### Final Code of Root Module

```sh
module "iam-1" {
    source = "./modules/iam-1"
}

module "iam-2" {
    source = "./modules/iam-2"
}

moved {
  from = aws_iam_user.lb
  to   = module.iam-1.aws_iam_user.lb
}


moved {
  from = aws_iam_user.lb2
  to   = module.iam-2.aws_iam_user.lb2
}
```

### Commands Used
```sh
terraform init
terraform plan
terraform apply -auto-approve

terraform state list
```