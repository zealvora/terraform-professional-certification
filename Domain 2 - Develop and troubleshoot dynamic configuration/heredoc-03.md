### Base Code Used

```sh
resource "local_file" "basic" {
    filename = "basic.txt"
    content = <<EOT
    This is Line 1
      This is Line 2
         This is Line 3
    EOT
}

resource "local_file" "indented" {
    filename = "indented.txt"
    content = <<-EOT
    This is Line 1
    This is Line 2
    This is Line 3
    EOT
}
```