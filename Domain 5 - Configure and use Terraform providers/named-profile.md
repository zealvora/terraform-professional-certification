
### Base Code Used
```sh
resource "aws_security_group" "allow_tls" {
  name        = "demo-firewall"
}
```

### Setting Right Profile in AWS CLI

```sh
aws configure --profile account02
aws configure list-profiles
```

### Specifying Named Profile

```sh
profile "aws" {
  profile = "account02"
  }

resource "aws_security_group" "allow_tls" {
  name        = "demo-firewall"
}
```

### Setting th Environement Variable

#### 1 - For Windows
```sh
set AWS_PROFILE=account02
echo %AWS_PROFILE
```

#### 2 - For Linux / macOS

```sh
export AWS_PROFILE=account02
echo $AWS_PROFILE
```