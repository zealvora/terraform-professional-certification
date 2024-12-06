
### Contents of instance-config.csv

```sh
instance_id,instance_type,ami
instance1,t2.micro,ami-1234
instance2,t2.small,ami-4576
instance3,t3.micro,ami-7891
instance4,m5.large,ami-2345
```

### Base Code

```sh
locals {
    instances = csvdecode(file("./instance-config.csv"))
}

resource "aws_instance" "web" {
  ami           = data.aws_ami.ubuntu.id
  instance_type = "t3.micro"
}
```

### Final Code

```sh
locals {
    instances = csvdecode(file("./instance-config.csv"))
}

locals {
    for = {for data in local.instances : data.instance_id => data}
}

output "for" {
    value = local.for
}

resource "aws_instance" "web" {
  for_each      = {for data in local.instances : data.instance_id => data}
  ami           = each.value.ami
  instance_type = each.value.instance_type
}
```