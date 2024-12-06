### Documentation Referenced:

https://developer.hashicorp.com/terraform/cli/config/config-file#explicit-installation-method-configuration


### Step 1 - Create Base Project Code (provider.tf)

```sh
provider "aws" {}

provider "google" {}

provider "local" {}
```

### Step 2 - Create a Folder for File System Mirror 

Use following command for Linux and macOS
```sh
mkdir filesystem-mirror
```

### Step 3: Mirror the Providers 
```sh
terraform providers mirror C:/filesystem-mirror
```

### Step 4: Content of Terraform RC File (Base)

For Linux, make sure to change the path accordingly.

```sh
provider_installation {
  filesystem_mirror {
    path    = "C:/filesystem-mirror"
    include = ["registry.terraform.io/hashicorp/*"]
  }
}
```

### Step 5: Content of Terraform RC File with Direct Method as well (Final) 

For Linux, make sure to change the path accordingly.

```sh
provider_installation {
  filesystem_mirror {
    path    = "C:/filesystem-mirror"
    include = ["registry.terraform.io/hashicorp/*"]
  }
  direct {
    include = ["registry.terraform.io/hashicorp/local"]
  }
}
```