### Base Code Used in Video (heredoc-2.tf)
```sh
resource "local_file" "this" {
    filename = "heredoc.txt"
    content = <<EOT
    This is Line 1
    This is Line 2
    This is Line 3
    EOT
}
```

### Testing Basic Heredoc Type
```sh
resource "local_file" "this" {
    filename = "heredoc.txt"
    content = <<EOT
    This is Line 1
      This is Line 2
         This is Line 3
    EOT
}
```
```sh
terraform apply -auto-approve
```

### Testing Indented Heredoc Type
```sh
resource "local_file" "indented" {
    filename = "indented.txt"
    content = <<-EOT
    This is Line 1
      This is Line 2
         This is Line 3
    EOT
}
```
```sh
terraform apply -auto-approve
```