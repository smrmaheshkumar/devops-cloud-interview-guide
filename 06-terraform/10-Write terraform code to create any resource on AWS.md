Below is a simple Terraform code example to create an **AWS S3 bucket** — one of the most commonly used AWS resources.

---

### ✅ **Terraform Code to Create an AWS S3 Bucket**

```hcl
# main.tf

provider "aws" {
  region = "us-east-1"  # Change as needed
}

resource "aws_s3_bucket" "my_bucket" {
  bucket = "my-unique-bucket-name-123456789"  # Must be globally unique
  acl    = "private"

  tags = {
    Name        = "MyBucket"
    Environment = "Dev"
  }
}
```

---

### 🧾 Steps to Use This Code

1. **Install Terraform**:
   [https://developer.hashicorp.com/terraform/downloads](https://developer.hashicorp.com/terraform/downloads)

2. **Configure AWS Credentials**:
   Set via AWS CLI or `~/.aws/credentials` file, or environment variables like:

   ```bash
   export AWS_ACCESS_KEY_ID="your-access-key"
   export AWS_SECRET_ACCESS_KEY="your-secret-key"
   ```

3. **Run Terraform Commands**:

   ```bash
   terraform init
   terraform plan
   terraform apply
   ```

---

### 📁 Optional: Recommended Folder Structure

```
terraform-s3/
├── main.tf
├── variables.tf     # (Optional) for input variables
├── outputs.tf       # (Optional) to output values
```
