
### Base Code

modules/iam/iam.tf
```sh
resource "aws_iam_user" "this" {
    name = "kplabs-user-1"
    count = 5
}
```
main.tf
```sh
module "iam" {
    source = "./modules/iam"
}
```

### Final Code:

modules/iam/iam.tf
```sh
resource "aws_iam_user" "this" {
    name = "kplabs-user-${count.index}"
    count = 5
}
```
main.tf
```sh
module "iam" {
    source = "./modules/iam"
}

moved {
    to   = module.iam.aws_iam_user.this[1]
    from = module.iam.aws_iam_user.this
}
```

### Commands Used
```sh
terraform init
terraform plan
terraform apply -auto-approve

terraform state list
```