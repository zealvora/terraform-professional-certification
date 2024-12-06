### Documentation Referred:

https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/autoscaling_group

### Final Code Snippet

```
resource "aws_launch_template" "this" {
    name     = "terraform-launch-template"
    image_id = "ami-06b21ccaeff8cd686"
    instance_type = "t2.micro"
    vpc_security_group_ids = ["sg-06dc77ed59c310f03"]
}

resource "aws_autoscaling_group" "bar" {
  availability_zones = ["us-east-1a","us-east-1b"]
  desired_capacity   = 2
  max_size           = 2
  min_size           = 1

  launch_template {
    id      = aws_launch_template.this.id
    version = "$Latest"
  }
}
```