When **two DevOps engineers attempt to update the same Terraform state file at once**, here's what happens — and why it can be **risky without state locking**:

---

### 🚨 Scenario: Two Engineers Run `terraform apply` Simultaneously

#### 🔴 Without Remote State Locking (e.g., using local backend or Git):

* Both users work on the same `terraform.tfstate` file.
* They run `terraform apply` at the same time.
* Since there's no locking mechanism, **race conditions** occur.
* Terraform might:

  * Overwrite or delete each other's changes.
  * Cause **state corruption**.
  * Leave infrastructure in a partially applied or inconsistent state.

> ❗ This is a **serious risk** in collaborative environments.

---

### ✅ With Remote State Locking (e.g., S3 + DynamoDB, Azure Blob Lease):

* Terraform locks the state file during `plan` or `apply`.
* If a second engineer tries to run Terraform:

  * They will see a message like:
    `Error acquiring the state lock. Another process is currently holding the state lock.`
* The second operation is **blocked until the first one finishes** and releases the lock.
* This **prevents corruption and ensures consistency**.

---

### 💡 Example Locking in AWS Backend:

```hcl
terraform {
  backend "s3" {
    bucket         = "my-terraform-state"
    key            = "prod/app.tfstate"
    region         = "us-east-1"
    dynamodb_table = "terraform-locks"  # Enables locking
  }
}
```

---

### 🛡️ Best Practices

* **Always use a remote backend** with state locking in shared/team environments.
* **Avoid manual edits** to the state file.
* **Enable versioning** and audit logging in your storage backend.

---
