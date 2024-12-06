
```sh
resource "random_integer" "this" {
  min = 1005
  max = 50000
}

resource "aws_s3_bucket" "example" {
  bucket = "kplabs-testing-bucket-${random_integer.this.result}"
}
```