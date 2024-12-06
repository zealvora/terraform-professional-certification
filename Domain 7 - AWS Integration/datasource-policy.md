### Documentation Referenced:

https://registry.terraform.io/providers/hashicorp/aws/latest/docs/data-sources/iam_policy_document

### Base Heredoc policy used in video (iam-datasource.tf)
```sh
resource "aws_iam_policy" "policy_custom_2" {
  name  = "test-iam-policy"

  policy = <<EOT
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Actions": [
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

### Final Policy Code used in video (iam-datasource.tf)

```sh
data "aws_iam_policy_document" "example" {

  statement {
    actions = ["ec2:Describe*"]
    resources = ["*"]
  }
}


resource "aws_iam_policy" "policy_custom" {
  name  = "tf-data-policy"

  policy = data.aws_iam_policy_document.example.json
}
```