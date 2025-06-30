Kodekloud Link: https://github.com/smrmaheshkumar/Certified-Kubernetes-Administrator-Kodekloud/blob/master/docs/03-Scheduling/14-DaemonSets.md


A **DaemonSet** is a type of Kubernetes resource that ensures a **copy of a pod runs on all (or selected) nodes** in a cluster.

---

### 🔧 **What does a DaemonSet do?**

A DaemonSet automatically manages the deployment of pods so that:

* One pod is **scheduled per node**
* When a new node is added to the cluster, the pod is **automatically added** to it
* When a node is removed, the pod is **deleted** from it

---

### 📦 **Use Cases of DaemonSets**

DaemonSets are typically used for **background system-level tasks**, such as:

* **Log collection agents** (e.g., Fluentd, Logstash)
* **Monitoring agents** (e.g., Prometheus Node Exporter)
* **Security/Antivirus agents**
* **Storage drivers** or **network plugins**

---

### 🛠️ Example YAML of a DaemonSet

```yaml
apiVersion: apps/v1
kind: DaemonSet
metadata:
  name: fluentd-logger
  namespace: kube-system
spec:
  selector:
    matchLabels:
      name: fluentd
  template:
    metadata:
      labels:
        name: fluentd
    spec:
      containers:
      - name: fluentd
        image: fluent/fluentd
```

---

### 🔍 Key Points

| Feature                | DaemonSet Behavior                     |
| ---------------------- | -------------------------------------- |
| Deployment Target      | All (or filtered) nodes in the cluster |
| Pod Scheduling         | One per node                           |
| Rolling Updates        | Supported (like Deployments)           |
| Node Lifecycle Changes | Pods added/removed automatically       |

---

Here’s a clear **comparison between DaemonSet and Deployment** in Kubernetes:

---

### 📊 **DaemonSet vs Deployment**

| Feature                    | **DaemonSet**                                              | **Deployment**                                       |
| -------------------------- | ---------------------------------------------------------- | ---------------------------------------------------- |
| **Purpose**                | Run **one pod per node** (usually system-level tasks)      | Run a **specified number of replicas** of a pod      |
| **Pod Count**              | 1 per node (or filtered nodes)                             | You define the number of replicas (e.g., 3, 5, etc.) |
| **Node Awareness**         | Yes – tightly tied to nodes                                | No – scheduler places pods anywhere in the cluster   |
| **Use Case Examples**      | Log collectors, monitoring agents, storage/network drivers | Web servers, APIs, applications                      |
| **Auto-Add on New Node**   | Yes – new pods created automatically on new nodes          | No – pods scale based on replica count               |
| **Scaling**                | Scales with node count                                     | Scales manually or automatically (HPA)               |
| **Rolling Update Support** | Yes                                                        | Yes                                                  |
| **Typical Namespace**      | Often in `kube-system`                                     | Usually in app-specific namespaces                   |

---

### 🧠 When to Use Which?

* ✅ Use **DaemonSet** when:

  * You need **one pod per node**
  * The service is **node-scoped** (e.g., metrics, log collection)
  * It’s a background/system service

* ✅ Use **Deployment** when:

  * You want to run **apps/services**
  * You want **flexible scaling** (replica count)
  * The app is **not tied to specific nodes**

---



