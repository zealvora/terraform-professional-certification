
### Base Code Used (tf-automate.tf)

```sh
resource "local_file" "foo" {
  content  = "foo!"
  filename = "hello.txt"
}
```

### Setting the ENV Variable in Windows (Temporarily)
```sh
set TF_IN_AUTOMATION=true
```

### Setting the ENV Variable in Linux / macOS
```sh
export TF_IN_AUTOMATION=true
```