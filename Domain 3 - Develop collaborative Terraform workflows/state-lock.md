### Base Code Used 

```sh
resource "time_sleep" "wait_300_seconds" {

  create_duration = "300s"
}

````

```sh
terraform apply -auto-approve
```