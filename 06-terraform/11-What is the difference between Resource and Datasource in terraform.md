### ❓ What is the difference between a Resource and a Data Source in Terraform?**

**In Terraform:**

* A **Resource** is used to **create, modify, or destroy** infrastructure components.
* A **Data Source** is used to **read information from existing** infrastructure **without modifying** it.

---

### 🔍 Detailed Comparison:

| Feature              | **Resource**                                | **Data Source**                       |
| -------------------- | ------------------------------------------- | ------------------------------------- |
| **Purpose**          | Manage and provision infrastructure         | Fetch or reference existing resources |
| **Lifecycle**        | Created, updated, or destroyed by Terraform | Read-only, no lifecycle management    |
| **Terraform Block**  | `resource` block                            | `data` block                          |
| **Creates Infra?**   | ✅ Yes                                       | ❌ No                                  |
| **Example Use Case** | Create an EC2 instance or S3 bucket         | Fetch an existing AMI or VPC ID       |

---

### 🔧 Examples:

#### 🟢 **Resource Example** – Create an S3 Bucket

```hcl
resource "aws_s3_bucket" "my_bucket" {
  bucket = "my-unique-bucket-name"
  acl    = "private"
}
```

#### 🔵 **Data Source Example** – Fetch the Latest Ubuntu AMI

```hcl
data "aws_ami" "ubuntu" {
  most_recent = true
  owners      = ["099720109477"] # Canonical

  filter {
    name   = "name"
    values = ["ubuntu/images/hvm-ssd/ubuntu-focal-20.04-amd64-server-*"]
  }
}
```

---

### 🎯 When to Use Each?

| Situation                                               | Use                                           |
| ------------------------------------------------------- | --------------------------------------------- |
| You want to **create** a new infrastructure component   | ✅ `resource`                                  |
| You want to **reference** something that already exists | ✅ `data` source                               |
| You're **importing** infrastructure into Terraform      | Start with `resource`, use `terraform import` |

---

### ✅ Summary (One-Liner)

> **"Resources manage infrastructure; data sources fetch info about existing infrastructure."**

---
