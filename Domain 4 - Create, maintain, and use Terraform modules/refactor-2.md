
### Base Code Used
```sh
resource "aws_instance" "a" {
    ami = "ami-0453ec754f44f9a4a"
    instance_type = "t2.micro"
}

resource "aws_instance" "b" {
    ami = "ami-0453ec754f44f9a4a"
    instance_type = "t2.micro"
}
```

### Final Code
```sh
resource "aws_instance" "c" {
    count = 2
    ami = "ami-0453ec754f44f9a4a"
    instance_type = "t2.micro"
}

#aws_instance.c[0]
#aws_instance.c[1]

moved {
    from = aws_instance.a
    to   = aws_instance.c[0]
}

moved {
    from = aws_instance.b
    to   = aws_instance.c[1]
}
```

### Commands Used
```sh
terraform init
terraform plan
terraform apply -auto-approve

terraform state list
```