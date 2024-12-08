
### Base code used in Video

```sh
resource "aws_instance" "staging" {
    ami = "ami-0e2c8caa4b6378d8c"
    instance_type = "t2.micro"
    count = 2
}
```

### Final Code with Moved Block
```sh
moved {
    from = aws_instance.prod[0]
    to   = aws_instance.staging[0]
}

moved {
    from = aws_instance.prod[1]
    to   = aws_instance.staging[1]
}

/*
moved {
    from = aws_instance.myec2
    to   = aws_instance.prod
}
*/
```

### Commands Used
```sh
terraform init
terraform plan
terraform apply -auto-approve

terraform state list
```