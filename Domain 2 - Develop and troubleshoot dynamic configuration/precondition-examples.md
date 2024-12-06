
### Example 1 - FileExists

```sh
resource "local_file" "example" {
  filename = "app.txt"
  content  = "Sample App Content"

  lifecycle {
    precondition {
      condition     = fileexists("${path.module}/db.txt")
      error_message = "The db.txt file must exist."
    }
  }
}
```

### Example 2 - Multiple Functions in Single Condition

```sh
resource "local_file" "example" {
  filename = "app.txt"
  content  = "Sample App Content"

  lifecycle {
    precondition {
      condition     = fileexists("${path.module}/db.txt") && file("${path.module}/db.txt") != ""
      error_message = "The db.txt file must exist."
    }
  }
}

```

### Example 3 - Referencing Variable in Precondition

Code 1 - Example 

```sh
variable "environment" {}

resource "local_file" "sensitive_data" {
  filename = "sensitive.txt"
  content  = "This is sensitive data"

  lifecycle {
    precondition {
      condition     = var.environment == "production"
      error_message = "Sensitive File can only be created in Production."
    }
  }
}
```


### Example 4 - Multiple Preconditions Block


```sh
variable "environment" {}

resource "local_file" "sensitive_data" {
  filename = "sensitive.txt"
  content  = "This is sensitive data"

  lifecycle {
    precondition {
      condition     = var.environment == "production"
      error_message = "Sensitive File can only be created in Production."
    }
    precondition {
      condition     = fileexists("${path.module}/app.txt")
      error_message = "app.txt must be present."
    }
  }
}
```