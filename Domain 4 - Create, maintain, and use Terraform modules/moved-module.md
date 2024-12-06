
```sh
module "s3-bucket" {
  source  = "terraform-aws-modules/s3-bucket/aws"
  version = "4.1.2"
  bucket = "kplabs-moved-practical"
}

resource "aws_s3_bucket" "moved" {
  bucket = "kplabs-moved-practical"
}

moved {
    from = aws_s3_bucket.moved
    to   = module.s3-bucket.aws_s3_bucket.this[0]
}
```