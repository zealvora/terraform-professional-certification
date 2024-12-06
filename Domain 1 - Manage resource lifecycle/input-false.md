
### input-false.tf (Base Code)

```sh
resource "local_file" "foo" {
  content  = "foo!"
  filename = var.file_name
}
```

```sh
terraform init
terraform apply -auto-approve
```

### Step 2 - Making filename variable

```sh
variable "file_name" {}

resource "local_file" "foo" {
  content  = "foo!"
  filename = var.file_name
}
```

```sh
terraform plan -input=false
```

### Step 3 - Final Code with S3 Backend

```sh
terraform {
  backend "s3" {
    bucket = "demo-user-sample-bucket"
    region = "ap-southeast-1"
  }
}

variable "file_name" {
  default = "hello.txt"
}

resource "local_file" "foo" {
  content  = "foo!"
  filename = var.file_name
}
```

```sh
terraform plan -input=false
```