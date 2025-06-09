# DevOps Interview Preparation Guide

This repository contains a structured collection of frequently asked DevOps interview questions along with concise, technical answers based on hands-on experience and real-world use cases. It covers a range of topics from Kubernetes and Terraform to CI/CD pipelines and Linux fundamentals.

---

## 📘 Table of Contents

1. [Introduction](#1-intro)
2. [Kubernetes Components](#2-kubernetes-components)
3. [Ansible Overview](#3-ansible-how-does-it-work)
4. [Helm Chart](#4-helm-chart--why-do-we-use)
5. [CI/CD Pipeline Walkthrough](#5-walkthrough-of-the-jobs-in-pipeline)
6. [Project Responsibilities](#6-what-were-your-responsibilities-in-the-prev-project)
7. [Deployment vs ReplicaSet](#7-deployment-vs-replicaset)
8. [Persistent Volume (PV) vs Persistent Volume Claim (PVC)](#8-pv-vs-pvc)
9. [ReplicaSet and PVC Resource Requests](#9-can-a-replicaset-request-for-pvc-if-it-out-of-memory)
10. [Linux Basics](#10-basic-qns-on-linux)
11. [Ansible Workflow](#11-ansible-how-does-ansible-work)
12. [Secret Management](#12-how-did-you-manage-secrets)
13. [Build/Test on Pull Requests](#13-do-you-have-buildtest-on-pr)
14. [Terraform: Commands & State Management](#14-terraform---terraform-commands-pipeline-structure)
15. [Database Connectivity in Pipelines](#15-how-do-you-connect-to-db-from-the-pipeline)
16. [Dockerfile Best Practices](#16-dockerfile-structure-multi-stage-or-single)
17. [Kubernetes Troubleshooting & Monitoring](#17-kubernetes-troubleshooting-commands-monitoring-tools)

---

## 1. Intro

Brief overview of DevOps tools and responsibilities in modern CI/CD workflows.

## 2. Kubernetes Components

- **kube-apiserver**
- **etcd**
- **kube-scheduler**
- **kube-controller-manager**
- **kubelet**
- **kube-proxy**

## 3. Ansible: How does it work?

- Agentless tool using SSH
- Uses YAML-based playbooks
- Push-based configuration management

## 4. Helm Chart – Why do we use?

- Package manager for Kubernetes
- Reusability, templating, and versioning
- Easy deployment and rollback of apps

## 5. Walkthrough of the Jobs in Pipeline

- Code checkout
- Static code analysis
- Docker image build & push
- Helm deployment to Kubernetes
- Automated tests (unit/integration)

## 6. What Were Your Responsibilities in the Previous Project?

- CI/CD pipeline creation
- Kubernetes deployment automation
- Infra provisioning with Terraform
- Secret and access management

## 7. Deployment vs ReplicaSet

| Feature         | Deployment | ReplicaSet |
|----------------|------------|------------|
| Abstraction     | High       | Low        |
| Rolling Updates | Yes        | No         |
| Use case        | App rollout| Ensuring pod count |

## 8. PV vs PVC

- **PV**: Cluster resource for storage
- **PVC**: User request for storage

## 9. Can a ReplicaSet Request for PVC if Out of Memory?

No, ReplicaSets manage pod counts, not resource provisioning. Resource limits must be pre-defined in pod specs.

## 10. Basic Qns on Linux

- File permissions (`chmod`, `chown`)
- Networking (`netstat`, `ss`)
- Process management (`top`, `ps`, `kill`)

## 11. Ansible – How Does It Work?

- Master uses inventory + playbooks
- Sends SSH commands to nodes
- Executes tasks idempotently

## 12. How Did You Manage Secrets?

- Kubernetes secrets
- HashiCorp Vault
- Encrypted Ansible Vault files
- GitHub Actions secrets

## 13. Do You Have Build/Test on PR?

Yes, using GitHub Actions/GitLab CI:
- Linting, Unit tests on PR
- Prevent merge on failure

## 14. Terraform – Commands & Pipeline Structure

- Commands: `init`, `plan`, `apply`, `destroy`
- Statefile stored in remote backend (e.g., Azure Blob/GCS)
- RBAC & network rules applied to restrict access
- Recovery via versioned storage or backup

## 15. How Do You Connect to DB from the Pipeline?

- Certificate-based authentication
- Secrets injected via environment variables
- Securely handled in secret managers

## 16. Dockerfile Structure – Multi-stage or Single?

- Multi-stage preferred for smaller images
- Stages: build → runtime

## 17. Kubernetes Troubleshooting Commands & Monitoring Tools

- `kubectl describe pod`
- `kubectl logs`
- `kubectl get events`
- Monitoring: Prometheus, Grafana, Loki, ELK
- Common Issues:
  - **CrashLoopBackOff**: App crash, config error
  - **ImagePullBackOff**: Invalid image name, auth issues

---

## 🛠️ Tools & Technologies

- Kubernetes
- Ansible
- Helm
- Terraform
- Docker
- GitHub Actions/GitLab CI
- Azure Blob / AWS S3 / GCS
- Prometheus & Grafana

---

## 📄 License

MIT

---

## 🙌 Contributions

Feel free to fork and contribute by opening a pull request!

