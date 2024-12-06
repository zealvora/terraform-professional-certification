### Documentation Referred:

https://registry.terraform.io/providers/hashicorp/aws/latest/docs/data-sources/caller_identity

### Code Used in Video

```sh
data "aws_caller_identity" "this" {}

output "this" {
    value = data.aws_caller_identity.this.*
}
```