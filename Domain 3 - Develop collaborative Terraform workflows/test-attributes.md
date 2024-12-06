## Base Code Used
test-attributes.tf
```sh
provider "aws" {
    region = "us-east-1"
}

variable "firewall_name" {
    default = "demo-firewall"
}

resource "aws_security_group" "this" {
  name        = var.firewall_name
}
```

demo.tftest.hcl

```sh
run "test_run" {}
```

### Learning 1 - Multiple Run Blocks in Test File

```sh
run "test_run" {}

run "test_run_2" {
  command = plan
}
```
### Learning 2 - Overriding Provider Block

demo.tftest.hcl

```sh
provider "aws" {
    region = "ap-south-1"
}

run "test_run" {}
```

### Learning 3 - Variables in Test Files

demo.tftest.hcl

```sh
provider "aws" {
    region = "ap-south-1"
}

variables {
    firewall_name = "test-firewall"
}

run "test_run" {}
```

