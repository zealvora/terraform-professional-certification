
### Step 1 - Create Base File (resolv.conf)

```sh
nameserver 8.8.8.8
nameserver 4.4.4.4
nameserver 10.77.0.2
```
### Step 2 - First Iteration of Template Example (resolv.tftpl)

```sh
nameserver ${dns_server_01}
nameserver ${dns_server_02}
nameserver ${dns_server_03}
```

### Step 3 - Terraform Code Used with Templates (template-dns.tf)

```sh
resource "local_file" "this" {
    content = templatefile("./resolv.tftpl",{
        dns_server_01="8.8.8.8",
        dns_server_02="4.4.4.4",
        dns_server_03="10.77.0.2"
    })
    filename = "./resolv-final.conf"
}
```
### Step 4 - Improve Terraform Template Using for expression (resolv.tftpl)

Remove the older contents of file and replace with the following code:

```sh
%{ for dns in dns_ips ~}
nameserver ${dns}
%{ endfor }
```

### Step 5 - Code Used for Second  Iteration of Template

Comment out / remove the previous code in template-dns.tf file

```sh
resource "local_file" "this" {
    content = templatefile("./resolv.tftpl",{
        dns_ips=["8.8.8.8","4.4.4.4","10.77.0.5"]
    })
    filename = "./resolv-final.conf"
}
```

## Dealing with Maps

### Step 1 - Create Terraform Code for Map based Template
```sh
resource "local_file" "map" {
    content = templatefile("./map.tftpl",{
        config = {"key1"="value1","key2"="value2"}
    })
    filename = "./final-map.conf"
}
```

### Step 2 - Create Template File for Maps (map.tftpl)
```sh
%{ for key,value in config}
set ${key} is ${value} 
%{ endfor }
```