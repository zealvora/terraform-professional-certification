
### Base Code Used (sg.tf)

```sh
resource "aws_security_group" "allow_tls" {
  name        = "demo-firewall"
}
```

### Test file (demo.tftest.hcl)

#### 1. For apply-based operations

```sh
run "demo_test" {}
```

#### 2. For plan-based operations

```sh
run "demo_test" {
  command = plan
}
```
