Monitoring a Kubernetes cluster is crucial for ensuring **performance, reliability, and early issue detection**. Here’s a comprehensive breakdown of **how to monitor Kubernetes**, including **what to monitor, tools to use, and best practices**. 

---

## 🎯 **What to Monitor in Kubernetes**

| Category                    | What to Monitor                                          |
| --------------------------- | -------------------------------------------------------- |
| **Cluster Health**          | Node status, pod availability, API server responsiveness |
| **Node Metrics**            | CPU, memory, disk, network                               |
| **Pod & Container Metrics** | Resource usage, restarts, liveness/readiness probes      |
| **Application Metrics**     | App-specific KPIs (e.g., HTTP error rates, latency)      |
| **Events & Logs**           | Pod logs, Kubernetes events, audit logs                  |
| **Network**                 | Pod-to-pod traffic, ingress/egress, DNS                  |
| **Security**                | Unauthorized access, role misuse, CVEs                   |

---

## 🛠️ **Tools for Monitoring Kubernetes**

### 📊 1. **Prometheus + Grafana** (Most Popular)

* **Prometheus**: Collects metrics from nodes, pods, services, etc.
* **Grafana**: Visualizes data with dashboards
* Use **kube-prometheus-stack** (Helm chart) for full setup

### 🧪 2. **Kubernetes Dashboard**

* Web UI for basic monitoring of cluster resources
* Shows nodes, pods, deployments, etc.

### 🔍 3. **Lens IDE**

* GUI tool to explore and monitor your cluster
* Shows real-time logs, metrics, events

### 📦 4. **ELK Stack (Elasticsearch, Logstash, Kibana)**

* Aggregates and visualizes **logs**
* Works with Fluentd/Fluent Bit or Filebeat for ingestion

### 🔐 5. **Falco** (Security Monitoring)

* Detects unexpected behavior (e.g., shell in container, host file access)

### 📈 6. **Kube-state-metrics**

* Exposes cluster state (Deployments, DaemonSets, etc.) as metrics for Prometheus

### ☁️ 7. **Cloud Provider Tools**

* **AWS CloudWatch**, **Azure Monitor**, **GCP Stackdriver** for managed clusters (EKS, AKS, GKE)

---

## 📦 Example: Monitoring with Prometheus & Grafana

1. Install via Helm:

```bash
helm repo add prometheus-community https://prometheus-community.github.io/helm-charts
helm repo update
helm install kube-prometheus prometheus-community/kube-prometheus-stack
```

2. Access Grafana:

```bash
kubectl port-forward svc/kube-prometheus-grafana 3000:80
```

* Open `http://localhost:3000`
* Default credentials: `admin / prom-operator`

---

## ✅ Best Practices

* Use **persistent storage** for metrics/logs
* Set **alerts** with Alertmanager or Grafana for resource issues
* Monitor **control plane components** (API server, etcd)
* Integrate **application-level monitoring** (e.g., using `/metrics` endpoint with Prometheus)

---
