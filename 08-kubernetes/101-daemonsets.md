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

Great question! Here's a clear and concise comparison of **StatefulSets vs DaemonSets** in Kubernetes.

---

## 🧱 **StatefulSet vs DaemonSet**

| Feature           | **StatefulSet**                                                                  | **DaemonSet**                                              |
| ----------------- | -------------------------------------------------------------------------------- | ---------------------------------------------------------- |
| **Purpose**       | Run **stateful applications** with persistent identity                           | Run **one pod per node**, usually for system-level tasks   |
| **Pod Identity**  | Each pod has a **stable name**, network ID, and storage (e.g., `web-0`, `web-1`) | All pods are **identical**, no unique identity             |
| **Scaling**       | You specify the number of replicas (e.g., 3)                                     | Automatically matches the number of nodes                  |
| **Use Cases**     | Databases (e.g., MongoDB, Cassandra, MySQL), Zookeeper                           | Log collectors, monitoring agents, storage/network plugins |
| **Storage**       | Supports **persistent volume claim templates** for each pod                      | Usually doesn't require persistent storage                 |
| **Startup Order** | Can **control startup/termination order** (important for clusters)               | No such ordering control                                   |
| **Pod Names**     | Predictable (`app-0`, `app-1`, ...)                                              | Randomly generated by Kubernetes                           |
| **Managed By**    | Kubernetes controller manager                                                    | Kubernetes controller manager                              |

---

## 🧠 When to Use

| Scenario                                                                    | Choose                         |
| --------------------------------------------------------------------------- | ------------------------------ |
| Need **1 pod per node** for background agents or monitoring?                | ✅ **DaemonSet**                |
| Need **unique identity + storage per pod** (e.g., database cluster)?        | ✅ **StatefulSet**              |
| Want to run the same pod many times without caring about order or identity? | ❌ Use a **Deployment** instead |

---

## 🎯 Example Use Cases

* ✅ **StatefulSet**:

  * Cassandra or MongoDB cluster
  * Zookeeper, Kafka brokers
  * Stateful apps needing identity and storage

* ✅ **DaemonSet**:

  * Fluentd/Logstash for log collection
  * Node-exporter for metrics
  * CNI (Container Network Interface) plugin

---



