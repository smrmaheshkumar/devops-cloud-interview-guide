### ❓ **Interview Question: What are Terraform Workspaces?**

### ✅ **Answer:**

**Terraform Workspaces** allow you to maintain **multiple states** for the same Terraform configuration, making it easier to manage **multiple environments** like `dev`, `stage`, and `prod` using a single codebase.

---

### 🔍 Why Use Workspaces?

By default, Terraform has a single workspace named `default`. When you use workspaces, each one gets its **own state file**, so:

* You can apply the same code to multiple environments.
* Resources don't clash because each workspace maintains separate state.
* It’s easier to test changes in a dev environment before promoting them to prod.

---

### 🧪 Example Use Case

You have one Terraform configuration that defines an EC2 instance. Using workspaces, you can spin up:

* One instance in `dev`
* Another in `prod`
  Each with **independent state** but using the **same code**.

---

### ⚙️ Terraform Workspace Commands

```bash
terraform workspace list              # List all workspaces
terraform workspace new dev           # Create a new workspace called "dev"
terraform workspace select dev        # Switch to "dev" workspace
terraform workspace show              # Show current workspace
terraform workspace delete dev        # Delete the workspace
```

---

### 📁 How It Works

Terraform stores each workspace’s state separately:

```
terraform.tfstate.d/
└── dev/
    └── terraform.tfstate
└── prod/
    └── terraform.tfstate
```

---

### ⚠️ Limitations

* Workspaces **do not isolate configuration** — only **state**.
* Not ideal for complex environment differences (e.g., different VPCs, regions).
* For complex setups, consider **separate directories** or **Terraform Cloud workspaces**.

---

### ✅ Best Practice

Use workspaces when:

* You want simple separation (same infra layout, different environments).
* You're not dealing with highly customized environment setups.

Use separate folders/modules when:

* You need environment-specific configurations or different providers.

---

### 🔁 Summary (One-liner)

> **"Terraform workspaces allow you to use the same code with different state files to manage multiple environments."**

---

Great! Here's a **practical example** of how to use **Terraform Workspaces** for managing `dev`, `qa`, and `stage` environments **with the same code**.

---

## 🏗️ Example: Using Workspaces for `dev`, `qa`, and `stage`

Let’s assume you are creating an AWS **S3 bucket**, and you want different buckets for each environment using workspaces.

---

### 🧾 `main.tf`

```hcl
provider "aws" {
  region = "us-east-1"
}

# Get the current workspace name (dev, qa, stage)
locals {
  environment = terraform.workspace
}

# Use workspace name in resource naming
resource "aws_s3_bucket" "env_bucket" {
  bucket = "my-app-${local.environment}-bucket-123456"  # must be globally unique
  acl    = "private"

  tags = {
    Environment = local.environment
    Owner       = "DevOps Team"
  }
}
```

---

### ⚙️ How to Use It

#### 1. **Initialize Terraform**

```bash
terraform init
```

#### 2. **Create and Use Workspaces**

```bash
terraform workspace new dev
terraform apply          # Creates the dev bucket

terraform workspace new qa
terraform apply          # Creates the qa bucket

terraform workspace new stage
terraform apply          # Creates the stage bucket
```

Each workspace creates a **separate S3 bucket**, like:

* `my-app-dev-bucket-123456`
* `my-app-qa-bucket-123456`
* `my-app-stage-bucket-123456`

All using the **same code** but maintaining **independent state files**.

---

### 📁 Terraform State Directory Structure (Auto-managed)

```
terraform.tfstate.d/
├── dev/
│   └── terraform.tfstate
├── qa/
│   └── terraform.tfstate
├── stage/
│   └── terraform.tfstate
```

---

### 🛡️ Best Practices

* Keep bucket names unique (S3 requires global uniqueness).
* Use `locals` and `terraform.workspace` to inject environment-specific logic.
* Store remote state (e.g., in S3 + DynamoDB) if multiple people are using Terraform.

---
