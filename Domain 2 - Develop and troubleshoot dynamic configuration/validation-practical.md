
```sh
variable "db_password" {
  type = string

  validation {
    condition = length(var.db_password) >= 12
    error_message = "Length of Database Password must be equal to or greater than 12 characters"
  }
}
```