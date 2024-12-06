### Documentation Referenced:

https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/iam_role_policy_attachment

### Step 1: Create a base IAM Role 
```sh
data "aws_iam_policy_document" "assume_role" {
  statement {
    effect = "Allow"

    principals {
      type        = "Service"
      identifiers = ["ec2.amazonaws.com"]
    }

    actions = ["sts:AssumeRole"]
  }
}

resource "aws_iam_role" "role" {
  name               = "test-role"
  assume_role_policy = data.aws_iam_policy_document.assume_role.json
}
```

### Step 2: Attach a Managed IAM Policy to IAM Role

```sh
resource "aws_iam_role_policy_attachment" "test-attach" {
  role       = aws_iam_role.role.name
  policy_arn = "arn:aws:iam::aws:policy/AmazonCloudWatchEvidentlyReadOnlyAccess"
}
```