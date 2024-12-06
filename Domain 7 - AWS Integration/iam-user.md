### Documentation Referred:

https://registry.terraform.io/providers/hashicorp/aws/latest/docs

### Base Examples
```sh
resource "aws_iam_user" "lb" {
  name = "terraform-user"
}

resource "aws_iam_user_login_profile" "example" {
  user    = "terraform-user"
  password_reset_required = "true"
}

resource "aws_iam_access_key" "lb" {
  user    = "terraform-user"
}
```

### Dependency Based Example

```sh
resource "aws_iam_user" "lb" {
  name = "terraform-user"
}

resource "aws_iam_user_login_profile" "example" {
  user    = aws_iam_user.lb.name
  password_reset_required = "true"
}

resource "aws_iam_access_key" "lb" {
  user    = aws_iam_user.lb.name
}
```



