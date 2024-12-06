### Documentation Referred:

https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/launch_template

### Base Examples

```sh
resource "aws_launch_template" "this" {
    name     = "terraform-launch-template"
    image_id = "ami-06b21ccaeff8cd686"
    instance_type = "t2.micro"
    vpc_security_group_ids = ["sg-06dc77ed59c310f03"]
}
```