
### Literal Quote
```sh
resource "local_file" "this" {
    content = "The name of best friends are \"Alice\", and \"Bob\""
    filename = "friends.txt"
}
```
### Literal Backslash

#### Base Linux Example
```sh
resource "local_file" "this" {
    content = "The path of Terraform is /root/kplabs-terraform"
    filename = "friends.txt"
}
```
#### Windows Example
```sh
resource "local_file" "this" {
    content = "The path of Terraform is C:\\kplabs-terraform"
    filename = "friends.txt"
}
```
### New Line 

```sh
resource "local_file" "this" {
    content = "The path of Terraform is \n C:\\kplabs-terraform"
    filename = "friends.txt"
}
```

### Tab Character 
```sh
resource "local_file" "this" {
    content = "Item 1:\tValue 1\nItem 2:\tValue 2"
    filename = "friends.txt"
}
```
### Tab Character with new Line
```sh
resource "local_file" "this" {
    content = "Item 1:\tValue 1\nItem 2:\tValue 2"
    filename = "friends.txt"
}
```