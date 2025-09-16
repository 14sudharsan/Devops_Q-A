# ðŸŒ Terraform Cheat Sheet  

## ðŸ”¹ Basics  
| Concept | Command / Syntax | Notes |
|---------|------------------|-------|
| Init project | `terraform init` | Downloads provider plugins & sets up working dir. |
| Validate config | `terraform validate` | Checks syntax correctness. |
| Plan changes | `terraform plan` | Shows what will change before applying. |
| Apply changes | `terraform apply` | Provisions infrastructure. |
| Destroy infra | `terraform destroy` | Tears down managed resources. |
| Format code | `terraform fmt` | Auto-formats `.tf` files. |
| Show state | `terraform show` | Displays current state. |
| List resources | `terraform state list` | Shows tracked resources. |
| Remove from state | `terraform state rm <resource>` | Stops tracking without deleting infra. |

---

## ðŸ”¹ File Structure  
| File | Purpose |
|------|---------|
| `main.tf` | Main configuration file (resources, providers). |
| `variables.tf` | Define input variables. |
| `outputs.tf` | Define outputs after apply. |
| `terraform.tfvars` | Default values for variables. |
| `provider.tf` | Provider configuration (AWS, Azure, GCP, etc.). |

---

## ðŸ”¹ Providers  
```hcl
provider "aws" {
  region = "us-east-1"
}
```

---

## ðŸ”¹ Resources  
```hcl
resource "aws_instance" "web" {
  ami           = "ami-123456"
  instance_type = "t2.micro"
}
```

---

## ðŸ”¹ Variables  
**variables.tf**
```hcl
variable "instance_type" {
  type    = string
  default = "t2.micro"
}
```
**usage**
```hcl
instance_type = var.instance_type
```
**terraform.tfvars**
```hcl
instance_type = "t3.medium"
```

---

## ðŸ”¹ Outputs  
```hcl
output "instance_ip" {
  value = aws_instance.web.public_ip
}
```

---

## ðŸ”¹ Data Sources  
```hcl
data "aws_ami" "ubuntu" {
  most_recent = true
  owners      = ["099720109477"]
  filter {
    name   = "name"
    values = ["ubuntu/images/*"]
  }
}
```

---

## ðŸ”¹ Meta-Arguments  
| Argument | Purpose |
|----------|---------|
| `count` | Create multiple instances with an index. |
| `for_each` | Create multiple instances from a map or set. |
| `depends_on` | Explicitly declare dependencies. |
| `lifecycle` | Control create/destroy/ignore changes. |

**Example (count):**
```hcl
resource "aws_instance" "web" {
  count = 3
  ami   = "ami-123456"
  instance_type = "t2.micro"
}
```

**Example (for_each):**
```hcl
resource "aws_instance" "web" {
  for_each = {
    dev  = "t2.micro"
    prod = "t3.medium"
  }
  instance_type = each.value
  tags = {
    Name = each.key
  }
}
```

---

## ðŸ”¹ Conditionals  
```hcl
instance_type = var.env == "prod" ? "t3.medium" : "t2.micro"
```

---

## ðŸ”¹ Loops  
```hcl
tags = { for idx, val in var.envs : idx => val }
```

---

## ðŸ”¹ Functions (Common)  
| Function | Example | Result |
|----------|---------|--------|
| `join` | `join(",", ["a","b","c"])` | `"a,b,c"` |
| `split` | `split(",", "a,b,c")` | `["a","b","c"]` |
| `lookup` | `lookup(var.map, "key", "default")` | Value of key or default |
| `length` | `length(var.list)` | Number of items |
| `file` | `file("creds.json")` | Reads file contents |
| `toset` / `tolist` | Convert list/set | Type conversion |

---

## ðŸ”¹ State Management  
- **Remote State (best practice):**  
```hcl
terraform {
  backend "s3" {
    bucket = "my-tf-state"
    key    = "infra/terraform.tfstate"
    region = "us-east-1"
  }
}
```

- Use **DynamoDB** for state locking with S3 backend.  

---

## ðŸ”¹ Best Practices  
âœ… Use **remote state** (S3 + DynamoDB, Azure Storage, GCS).  
âœ… Use **modules** to organize reusable code.  
âœ… Use **variables.tf + outputs.tf** for readability.  
âœ… Use **workspaces** for multiple environments.  
âœ… Always review `terraform plan` before `apply`.  