### Documentation Referenced:

https://developer.hashicorp.com/terraform/language/functions/jsonencode

https://developer.hashicorp.com/terraform/language/functions/jsondecode

### Base Command Used

```sh
terraform console
jsonencode({"hello"="world"})
```

### Base Code (jsonencode.tf)
```sh
resource "local_file" "with_jsonencode" {
  filename = "./json-encode.json"
  content  = jsonencode({
     name = "Alice
     age  =  30
     skills = ["Terraform","AWS","Azure"]
  })
}
```

```sh
resource "local_file" "with_jsonencode" {
  filename = "./json-encode.json"
  content  = jsonencode(["Terraform", "AWS", "Azure"])
}
```

## JSON-DECODE Practical

Contents of sample.json file 

```sh
{
    "name": "Alice Katherine",
    "age": 30,
    "skills": ["Terraform", "AWS", "Ansible"],
    "active": true,
    "projects": [
      {
        "name": "Project X",
        "status": false
      },
      {
        "name": "Project Y",
        "completed": true
      }
    ]
  }
```


```sh
locals {
    contents = file("./sample.json")
    decode   = jsondecode(local.contents)
}

output "jsondecode" {
    value = local.decode
}
```
```sh
terraform apply -auto-approve
```