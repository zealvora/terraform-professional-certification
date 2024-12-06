
### demo.csv file contents
```sh
instance_id,instance_type,ami
instance1,t2.micro,ami-1234
instance2,t2.small,ami-4576
instance3,t3.micro,ami-7891
instance4,m5.large,ami-2345
```

### Commands Used In Video

```sh
terraform console
file("./demo.csv)
csvdecode(file("./demo.csv))
```

### Documentation Referenced:

https://developer.hashicorp.com/terraform/language/functions/csvdecode

```sh
csvdecode("a,b,c\n1,2,3\n4,5,6")
```