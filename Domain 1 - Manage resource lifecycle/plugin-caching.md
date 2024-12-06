### Documentation Referenced:

https://developer.hashicorp.com/terraform/cli/config/config-file

### Important Details to Remember

1. Find the AppData path for Windows OS (PowerShell)

```sh
$env:APPDATA
```
2. Terraform File RC File Name

Windows       = terraform.rc
Linux / macOS = .terraformrc

3. Sample Resource File Used for Practical (sg.tf)

```sh
resource "aws_security_group" "dev" {
  name        = "dev-sg"
}
```
### Windows Config Used

```sh
plugin_cache_dir   = "C:/tf-plugin-cache"
plugin_cache_may_break_dependency_lock_file = true

```

### Linux Config Used 
### Sample Content of Terraform RC File

nano ~/.terraformrc
```sh
plugin_cache_dir   = "$HOME/tf-plugin-cache"
plugin_cache_may_break_dependency_lock_file = true
```
