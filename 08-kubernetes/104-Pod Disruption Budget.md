### 🛡️ **What is a Pod Disruption Budget (PDB)?**

A **Pod Disruption Budget (PDB)** in Kubernetes is a policy that **limits the number of pods of a replicated application that can be down simultaneously** during **voluntary disruptions**. 

---

### 💥 What Are *Voluntary Disruptions*?

These are **planned disruptions**, such as:

* Node draining (`kubectl drain`)
* Cluster upgrades
* Manual pod eviction

> 🛑 PDB **does not protect against involuntary disruptions**, like node crashes or hardware failures.

---

### 🎯 Purpose of PDB

To ensure **high availability** of critical applications by:

* Preventing too many pods from going offline at once
* Helping maintain **minimum availability** during operations like maintenance or upgrades

---

### 🔧 Example PDB YAML

```yaml
apiVersion: policy/v1
kind: PodDisruptionBudget
metadata:
  name: my-app-pdb
spec:
  minAvailable: 2  # At least 2 pods must remain available
  selector:
    matchLabels:
      app: my-app
```

Alternatively, you can use `maxUnavailable`:

```yaml
spec:
  maxUnavailable: 1  # No more than 1 pod can be unavailable
```

---

### 📌 Key Fields

| Field            | Description                                                  |
| ---------------- | ------------------------------------------------------------ |
| `minAvailable`   | Minimum number or percentage of pods that must be up         |
| `maxUnavailable` | Maximum number or percentage of pods that can be unavailable |
| `selector`       | Matches the pods the PDB applies to                          |

---

### 🧠 Example Scenario

If you have a Deployment with **5 replicas** and define:

```yaml
minAvailable: 3
```

Then:

* Only **2 pods** can be voluntarily disrupted at any time
* If someone tries to drain a node that would cause 3 pods to go down, **Kubernetes blocks the operation**

---

### ✅ When to Use PDB?

* For **stateful or critical apps** (like databases, web servers, etc.)
* During **cluster upgrades** to prevent service disruption
* When using **automated scaling or maintenance tools**

---

Would you like a **visual or diagram explanation** of how PDB works during node draining?

![image](https://github.com/user-attachments/assets/74720487-cbcd-4ca7-8ddb-eb9214be1536)

