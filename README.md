# k8s-elk-stack

This repository contains the Kubernetes manifests and configurations to deploy the **ELK Stack (Elasticsearch, Kibana)** along with **Filebeat** on **Amazon EKS**. This setup enables centralized logging by collecting logs from all pods, containers, and nodes inside your EKS cluster, and visualizing them in Kibana.

---

## 📦 Stack Overview

- **Elasticsearch**: Stores and indexes all logs.
- **Kibana**: Provides a UI for exploring and visualizing logs.
- **Filebeat**: Runs as a DaemonSet on all EKS worker nodes to collect logs and send them directly to Elasticsearch.

---

## 🧱 Architecture

+----------------+ +------------+ +------------------+ +-------------+ | EKS Cluster | --> | Filebeat | --> | Elasticsearch | --> | Kibana | | (Pods, Nodes) | | (DaemonSet)| | (StatefulSet) | | (Deployment)| +----------------+ +------------+ +------------------+ +-------------+


- Filebeat tails logs from `/var/log/containers/` and system logs.
- Logs are directly shipped to Elasticsearch.
- Kibana offers a dashboard to search, filter, and visualize the logs.

---

## 📂 Folder Structure

```bash
k8s-elk-stack/
├── elasticsearch/
│   └── elasticsearch-statefulset.yaml
├── kibana/
│   └── kibana-deployment.yaml
├── filebeat/
│   ├── filebeat-config.yaml
│   └── filebeat-daemonset.yaml
├── namespace.yaml
└── README.md
```
---

## 🚀 Deployment Steps

Set up EKS cluster (if not already done).

Clone this repository:


git clone https://github.com/ashreesee/k8s-elk-stack.git
cd k8s-elk-stack
Apply the Kubernetes namespace (if using a custom namespace):


kubectl apply -f namespace.yaml
Deploy Elasticsearch:
kubectl apply -f elasticsearch/elasticsearch-statefulset.yaml
Deploy Kibana:
kubectl apply -f kibana/kibana-deployment.yaml
Deploy Filebeat:
kubectl apply -f filebeat/filebeat-config.yaml
kubectl apply -f filebeat/filebeat-daemonset.yaml

🔍 Accessing Kibana
To access the Kibana dashboard locally:

kubectl port-forward service/kibana 5601
Then open: http://localhost:5601
---
## 📑 What’s Being Collected?
Filebeat automatically collects:

Application container logs (/var/log/containers/*.log)

System logs from Kubernetes components like kubelet, kube-proxy, etc.

Node-level logs

These are indexed in Elasticsearch and made queryable in Kibana.
---
## 📈 Using Kibana
Go to the "Discover" tab to browse logs.

Use KQL (Kibana Query Language) to filter and search.

Create visualizations and dashboards for error rates, app logs, etc.

Example query to find all error logs:

pgsql
Copy
Edit
log.level: "error"
---
## ✅ Requirements
A running Amazon EKS cluster

kubectl configured to access the cluster

Sufficient node resources for Elasticsearch (CPU/memory/disk)
---
## 🔧 Future Improvements
 Add Persistent Volume Claims (PVCs) for Elasticsearch

 Configure Ingress or LoadBalancer for Kibana access

 Add alerting with Watcher or Kibana alerts

 Pre-configure Kibana dashboards and index patterns