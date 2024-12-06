### Documentation Referred:

https://registry.terraform.io/providers/hashicorp/random/latest/docs/resources/integer

### Base Code 
```sh
resource "random_integer" "this" {
    min = 100
    max = 1000
}
output "this" {
    value = random_integer.this.id
}
```
### Final Code
```sh
resource "aws_s3_bucket" "this" {
    bucket = "kplabs-bucket-${random_integer.this.result}"
}

output "this" {
    value = random_integer.this.id
}
```