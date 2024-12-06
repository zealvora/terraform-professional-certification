
### Base Code Used

s3.tf 

```sh
variable "s3_bucket_name" {
  default = "sample-kplabs-bucket"
}

resource "aws_s3_bucket" "example" {
  bucket = var.s3_bucket_name
}
```

demo.tftest.hcl

```sh
run "test_run" {}

### Final Code Used in the Test File

```sh
run "test_run" {
    command = plan

    assert {
        condition = length(var.s3_bucket_name) > 3
        error_message = "S3 bucket name must be greater than 3 characters"
    }
}
```