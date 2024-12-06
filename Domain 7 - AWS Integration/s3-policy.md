### Documentation Referenced:

https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/s3_bucket_policy



### Point to Note

Make sure to change the bucket name and Account Number in the below code.

```sh
resource "aws_s3_bucket" "example" {
  bucket = "kplabs-bucket-0121423"
}

resource "aws_s3_bucket_policy" "allow_access_from_another_account" {
  bucket = aws_s3_bucket.example.id
  policy = data.aws_iam_policy_document.allow_access_from_another_account.json
}

data "aws_iam_policy_document" "allow_access_from_another_account" {
  statement {
    principals {
      type        = "AWS"
      identifiers = ["042025557788"]
    }

    actions = [
      "s3:GetObject",
      "s3:ListBucket",
    ]

    resources = [
      aws_s3_bucket.example.arn,
      "${aws_s3_bucket.example.arn}/*",
    ]
  }
}
```