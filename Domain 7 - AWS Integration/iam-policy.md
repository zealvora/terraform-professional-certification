### Documentation Referred:

https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/iam_policy

https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/iam_user_policy

### Customer Managed Policy

```sh
resource "aws_iam_policy" "policy" {
  name        = "terraform-managed-policy"

  policy = jsonencode({
    Version = "2012-10-17"
    Statement = [
      {
        Action = [
          "ec2:Describe*",
        ]
        Effect   = "Allow"
        Resource = "*"
      },
    ]
  })
}
```

### Inline Policy - jsonencode Approach

```sh
resource "aws_iam_user_policy" "lb_ro" {
  name = "terraform-inline-policy"
  user = "terraform"

  policy = jsonencode({
    Version = "2012-10-17"
    Statement = [
      {
        Action = [
          "ec2:Describe*"
        ]
        Effect   = "Allow"
        Resource = "*"
      },
    ]
  })
}
```

### Customer Managed Policy - Heredoc Approach

```sh
resource "aws_iam_policy" "policy_custom" {
  name  = "test-iam-policy"

  policy = <<EOT
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Action": [
                "ec2:Describe*"
            ],
            "Effect": "Allow",
            "Resource": "*"
        }
    ]
}
EOT
}
```

### File Based Approach

```sh
resource "aws_iam_policy" "policy_file" {
  name  = "file-based-policy"
  policy = file("./ec2-describe.json")
}
```