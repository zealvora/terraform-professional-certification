### Documentation Referenced:

https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/iam_role

### Code Used (iam-role.tf)

```sh
resource "aws_iam_role" "test_role" {
  name = "terraform-iam-role"
  assume_role_policy = jsonencode({
    Version = "2012-10-17"
    Statement = [
      {
        Action = "sts:AssumeRole"
        Effect = "Allow"
        Sid    = ""
        Principal = {
          Service = "ec2.amazonaws.com"
        }
      },
    ]
  })
}
```