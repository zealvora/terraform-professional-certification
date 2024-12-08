
### Base Code Used

```sh
resource "aws_instance" "a" {
    ami = "ami-0453ec754f44f9a4a"
    instance_type = "t2.micro"
}

resource "aws_instance" "b" {
    ami = "ami-0e2c8caa4b6378d8c"
    instance_type = "t2.micro"
}
```


### Final Code Used

```sh
locals {
    instance_data = {
        first_ec2 = {
            ami = "ami-0453ec754f44f9a4a"
            instance_type = "t2.micro"
        }
        second_ec2 = {
            ami = "ami-0e2c8caa4b6378d8c"
            instance_type = "t2.micro"
        }
    }
}

#output "test" {
#    value = local.instance_data["first_ec2"]["ami"]
#}


resource "aws_instance" "c" {
    for_each = local.instance_data
    ami = each.value.ami
    instance_type = each.value.instance_type
}


moved {
    from = aws_instance.a
    to   = aws_instance.c["first_ec2"]
}

moved {
    from = aws_instance.b
    to   =  aws_instance.c["second_ec2"]
}
```

### Commands Used
```sh
terraform init
terraform plan
terraform apply -auto-approve

terraform state list
```