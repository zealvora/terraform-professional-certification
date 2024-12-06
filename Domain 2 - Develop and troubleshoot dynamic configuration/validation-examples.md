
### Example 1

```sh
resource "aws_instance" "myec2" {
    ami = "ami-123"
    instance_type = var.instance_type
}

variable "instance_type" {
  type = string

  validation {
    condition     = contains(["t3.micro", "t3.medium", "m5.large"], var.instance_type)
    error_message = "Invalid instance type. Choose from: t3.micro, t3.medium, m5.large"
  }
}
```

### Example 2

```sh
variable "email_id" {
  type = string
  
  validation {
    condition     = can(regex("^\\S+@\\S+\\.\\S+$", var.email_id))
    error_message = "The email must be a valid email address"
  }
}
```

### Example 3

```sh
variable "image_id" {
  type        = string
  description = "The id of the machine image (AMI) to use for the server."

  validation {
    condition     = length(var.image_id) > 4 && substr(var.image_id, 0, 4) == "ami-"
    error_message = "The image_id value must be a valid AMI id, starting with \"ami-\"."
  }
}
```