### Base Code Used (pre-condition.tf)

```sh
data "aws_ec2_instance_type" "example" {
  instance_type = "t2.micro"
}

resource "aws_instance" "example" {
  instance_type = "t2.micro"
  ami           = "ami-066784287e358dad1"
  }
```

### Final Code

```sh
data "aws_ec2_instance_type" "example" {
  instance_type = "t3.micro"
}

output "instance_type" {
  value = data.aws_ec2_instance_type.example.free_tier_eligible
}



resource "aws_instance" "example" {
  instance_type = "t2.micro"
  ami           = "ami-066784287e358dad1"

  lifecycle {

    precondition {
      condition = data.aws_ec2_instance_type.example.free_tier_eligible
      error_message = "Instance Type is not part of free tier"
    }

    postcondition {
      condition = self.public_dns == ""
      error_message = "Public IPV4 or DNS is mandatory for this server"
    }
  }
  }
```