
### Base Example

```sh
resource "local_file" "this" {
    content = "This is Line 1\nThis is Line 2\nThis is Line 3"
    filename = "sample-file.txt"
}
```

```sh
resource "local_file" "this" {
    content = "This is Line 1\nNow it becomes a multi-line document\nThis is getting little confusing to read"
    filename = "sample-file.txt"
}
```

### Heredoc Example
```sh
resource "local_file" "this" {
    filename = "heredoc.txt"
    content = <<-ABC
    This is Line 1
    Now it becomes a multi-line document
    This is getting little confusing to read
    ABC
}
```