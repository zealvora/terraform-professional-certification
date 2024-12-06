### Documentation Referenced:

https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/s3_bucket

https://docs.aws.amazon.com/AmazonS3/latest/userguide/bucketnamingrules.html

### Base Code Used for Example 1:
```sh
terraform {
  required_providers {
    aws = "~>5.6"
  }
}

resource "aws_iam_user" "dev" {
    name = kplabs-user-01#
}
```
### Base Code Used for Example 2:

```sh
terraform {
  required_providers {
    aws = "~>5.6"
  }
}


