# KubeForge (BYOI Kubernetes Platform)

[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](https://opensource.org/licenses/MIT)
[![PRs Welcome](https://img.shields.io/badge/PRs-welcome-brightgreen.svg)](#contributing)

KubeForge is an open-source, agent-driven "Bring Your Own Infrastructure" (BYOI) platform. It securely bootstraps Kubernetes clusters on raw, unmanaged VPS nodes from any cloud provider and provides a centralized marketplace for one-click Helm chart deployments.

## 🚀 The Problem We Solve
Managed Kubernetes services (like EKS or GKE) are expensive, while DIY bare-metal provisioning is complex and error-prone. Traditional cluster provisioners require inbound root SSH access, creating significant security vulnerabilities. 

KubeForge bridges the gap between cheap raw compute and robust managed ecosystems. It uses a lightweight, outbound agent to eliminate SSH risks, automating the orchestration of dispersed VPS nodes into a unified Kubernetes cluster.

## ✨ Key Features
* **Zero-SSH Provisioning:** Nodes connect securely to the control plane via an outbound tunnel using the KubeForge Agent.
* **Cross-Provider Networking (CNI):** Seamlessly span clusters across different cloud providers (AWS, Hetzner, DigitalOcean) using a secure overlay network.
* **Integrated Service Catalog:** A built-in marketplace for DevOps engineers to publish, version, and manage ready-to-run Helm charts.
* **Self-Service Dashboard:** Developers can monitor cluster health and deploy databases, caches, and applications with a single click.
* **Low Resource Footprint:** Designed specifically for edge and low-resource VPS environments.

## 🏗️ Architecture Overview
1. **The Control Plane:** Hosts the management UI, the cluster bootstrapper API, and the Service Catalog registry.
2. **The KubeForge Agent:** A lightweight binary executed on the target VPS. It dials back to the Control Plane to receive its provisioning payload and node registration instructions.
3. **The Cluster:** Once bootstrapped, the nodes operate autonomously, ensuring workloads remain highly available even if the Control Plane tunnel temporarily drops.

## 📦 Getting Started

### Prerequisites
* A server to host the KubeForge Control Plane (Docker required).
* One or more raw Ubuntu/Debian VPS instances (Minimum 2GB RAM).

### 1. Launch the Control Plane
```bash
docker run -d -p 8080:8080 -p 8443:8443 --name kubeforge-cp kubeforge/control-plane:latest
```

### 2. Connect a Worker Node
From the KubeForge UI, generate an agent token. SSH into your raw VPS and run:
```bash
curl -sfL https://your-kubeforge-cp.com/agent.sh | sh -s - --token YOUR_TOKEN
```
Your node will automatically appear in the dashboard and begin the Kubernetes bootstrapping process.

## 🗺️ Roadmap
- [x] Agent-based outbound node registration
- [x] Automated single-node K3s/K8s bootstrapping
- [ ] Cross-provider overlay networking (WireGuard/Cilium integration)
- [ ] Service Catalog UI for Helm deployments
- [ ] Zero-downtime rolling upgrades for worker nodes

## 🤝 Contributing
We welcome contributions from DevOps engineers, SREs, and Go/React developers! Whether it's adding new infrastructure connectors, improving the agent resilience, or expanding the Helm catalog, please check out our [Contributing Guidelines](CONTRIBUTING.md).

## 👨‍💻 Maintainers
* **Hamed Sadeghinezhad** - *Software Engineer & Architect*

---
*If you find this project useful, please consider giving it a ⭐ on GitHub!*
