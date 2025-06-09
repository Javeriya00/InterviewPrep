---

```markdown
# DevOps Interview Preparation – Azure DevOPs Engineer Role

This repository is a curated list of advanced DevOps interview questions and concepts covering Kubernetes, Azure, CI/CD pipelines, infrastructure as code, containerization, and security practices. It is especially useful for roles involving Azure, GitHub/GitLab CI, and container orchestration.

---

## 📘 Table of Contents

1. [Subnet & Logical Isolation](#1-subnet--logical-isolation)
2. [Network Security Groups (NSG)](#2-logical-isolation-using-nsg)
3. [Deployment vs ReplicaSet](#3-deployment-vs-replicaset)
4. [Deployment+PV vs ReplicaSet+PV](#4-is-deploymentpv--replicasetpv)
5. [ReplicaSet and PVC](#5-can-a-replicaset-request-for-pvc)
6. [Ansible Role Structure](#6-ansible-role-folder-structure)
7. [Helm Chart Structure](#7-helm-chart-structure--how-does-helm-work)
8. [Terraform State Recovery](#8-retrieve-deleted-terraform-statefile)
9. [CIDR Calculations](#9-how-many-ips-in-10035622)
10. [GitHub vs GitLab](#10-github-vs-gitlab)
11. [Kubernetes Deployment Strategies](#11-kubernetes-deployment-strategy)
12. [Service Communication in K8s](#12-how-do-services-communicate)
13. [Service Identification](#13-how-are-services-identified)
14. [Dockerfile – Entrypoint vs CMD](#14-dockerfile-structure--entrypoint-vs-cmd)
15. [Deploying .NET/Python Apps](#15-deploy-net-or-python-app-on-server)
16. [Secrets Management in Pipelines](#16-manage-secrets-in-pipeline)
17. [Build Flow in Branching](#17-build-strategy-across-branches)
18. [Common Secrets in GitLab](#18-where-to-define-common-secrets-in-gitlab)
19. [CI/CD Pipeline Flow & Fortify](#19-walkthrough-of-pipeline--fortify-dast)
20. [SAST vs DAST](#20-what-do-sast--dast-scan)
21. [Image Hardening](#21-how-did-you-harden-docker-image)
22. [Azure Integration](#22-acr-kubernetes-network-settings-storage)
23. [Azure Migrate Capabilities](#23-what-does-azure-migrate-offer)
24. [Build/Unit Tests on PR](#24-do-you-have-build--unit-tests-on-pr)
25. [IIS Server & `.csproj` File](#25-idea-on-iis--csproj-file)
26. [Helm Values File](#26-what-to-define-in-helm-valuesyaml)

---

## 1. Why Is a Subnet Required?

A **subnet (subnetwork)** is used for **logical isolation** within a larger network.

- It segments a network into smaller groups for manageability and security.
- Helps apply **access controls**, **routing rules**, and **network segmentation**.
- Common in cloud networking (e.g., Azure VNet subnets).

> Subnets provide **logical**, not physical, isolation of resources.

---

## 2. How Do You Achieve Logical Isolation?

Logical isolation in a cloud or on-premises network is commonly achieved with:

- **Network Security Groups (NSGs)**: Define inbound/outbound traffic rules.
- **Firewalls & route tables**: Restrict or redirect traffic between subnets.
- **Private endpoints**: Limit access to internal services.
- **RBAC**: Limit which identities can interact with network resources.

> In Azure, **NSGs** are the key resource for subnet-level traffic control and isolation.

---

## 3. Deployment vs ReplicaSet

| Feature               | Deployment                              | ReplicaSet                            |
|------------------------|------------------------------------------|----------------------------------------|
| Purpose                | Manages the lifecycle of applications    | Ensures a specified number of pods run |
| Rolling Updates        | ✅ Supported                              | ❌ Not supported                        |
| Rollbacks              | ✅ Supported                              | ❌ Not supported                        |
| Use Case               | Application lifecycle management         | Pod replica management                 |
| Abstraction Level      | High-level controller                    | Low-level controller                   |

> Deployments wrap ReplicaSets and offer features like rollouts and rollback.

---

## 4. Is Deployment + PV Equivalent to ReplicaSet + PV?

**No.** While both can use a Persistent Volume (PV) via a Persistent Volume Claim (PVC), only **Deployment**:

- Supports **rolling updates**
- Handles **versioning and rollbacks**
- Offers full **lifecycle management**

> Deployment + PV is a **more complete and production-ready** approach.

---

## 5. Can a ReplicaSet Request for PVC?

Not directly.

- ReplicaSets **manage Pods**.
- If a Pod in the ReplicaSet references a PVC in its volume spec, the Pod will attempt to mount it.
- The PVC must already exist or be dynamically provisioned.

> It’s the **Pod spec** under a ReplicaSet that handles PVCs — the ReplicaSet itself doesn’t directly request them.

---

## 6. Ansible Role Folder Structure

```

roles/
└── myrole/
├── defaults/
├── files/
├── handlers/
├── meta/
├── tasks/
├── templates/
└── vars/

````

## 7. Helm Chart Structure – How Does Helm Work?

Helm is a package manager for Kubernetes. It simplifies deployment by using templated YAML files called charts.

### 📁 Basic Helm Chart Structure:

mychart/
├── Chart.yaml # Chart metadata (name, version, dependencies)
├── values.yaml # Default configuration values
├── templates/ # Kubernetes manifest templates
│ ├── deployment.yaml # Deployment resource template
│ ├── service.yaml # Service resource template
│ ├── ingress.yaml # Optional Ingress resource
│ ├── _helpers.tpl # Reusable helper templates and naming logic
│ ├── configmap.yaml # Optional ConfigMap
│ ├── secret.yaml # Optional Secret
│ ├── hpa.yaml # Optional Horizontal Pod Autoscaler
│ └── NOTES.txt # Post-installation output

# Set variables
ACR_LOGIN_SERVER=myregistry.azurecr.io
IMAGE_NAME=myapp
IMAGE_TAG=${{ github.run_id }}

# Use Helm to upgrade or install the release with the latest image tag
helm upgrade --install myapp ./helm/mychart \
  --namespace production \
  --set image.repository=$ACR_LOGIN_SERVER/$IMAGE_NAME \
  --set image.tag=$IMAGE_TAG \
  --values helm/values-prod.yaml

### 🧩 How Does Helm Work?

1. **Templating**: Uses Go templates (`{{ }}` syntax) in the `templates/` folder.
2. **Rendering**: At runtime, Helm combines templates with values from:
   - `values.yaml`
   - CLI flags (`--set key=value`)
   - External values files (`-f custom-values.yaml`)
3. **Packaging**: Charts are packaged into `.tgz` files and can be stored in Helm repositories.
4. **Release Management**:
   - Helm tracks each installation as a release.
   - Supports upgrades, rollbacks, and history tracking.

---

## 8. Retrieve Deleted Terraform Statefile

- Use **remote backend versioning** (e.g., Azure Blob, S3)
- Restore previous version via console/CLI
- Enforce **soft delete** and **state locking**

9. There Are How Many IPs in 10.0.3.56/22?
CIDR /22 = 32 - 22 = 10 bits for host addresses

2¹⁰ = 1024 IPs total

Usable IPs = 1022 (1 for network, 1 for broadcast)

Range: 10.0.0.0 – 10.0.3.255

So, 10.0.3.56 lies within a subnet that holds 1024 addresses

## 10. GitHub vs GitLab

| Feature       | GitHub          | GitLab               |
|---------------|-----------------|-----------------------|
| CI/CD         | GitHub Actions  | Built-in CI/CD        |
| Hosting       | GitHub Cloud    | Self-hosted supported |
| Security      | Secret scanning | Built-in SAST/DAST    |

## 11. Kubernetes Deployment Strategy

- Rolling update
- Recreate
- Canary (via Argo Rollouts)
- Blue-Green

## 12. How Do Services Communicate?

- Through Kubernetes **ClusterIP** or **DNS**
- Internal DNS: `servicename.namespace.svc.cluster.local`

## 13. How Are Services Identified?

- Using **labels** and **selectors**

## 14. Dockerfile Structure – Entrypoint vs CMD

```dockerfile
ENTRYPOINT ["python"]
CMD ["app.py"]
````

* `ENTRYPOINT`: Fixed binary
* `CMD`: Arguments to ENTRYPOINT

## 15. Deploy .NET or Python App on Server

* Use **IIS** for .NET with `.csproj` and MSBuild
* Use **Gunicorn/UWSGI** for Python, run behind Nginx

## 16. Manage Secrets in Pipeline

* GitHub: Repository secrets
* GitLab: CI/CD variables (masked/protected)
* Vault: For advanced secret rotation

## 17. Build Strategy Across Branches

* Can use **promotion-based** (same artifact) or **per-branch builds**
* Safer to rebuild for every environment

## 18. Where to Define Common Secrets in GitLab

* **Group-level CI/CD variables**
* Available across all projects in the group

## 19. Walkthrough of Pipeline – Fortify DAST

* Stages: Build → Scan → Test → Deploy
* Fortify:

  * SAST during **code/build stage**
  * DAST post-deployment (optional)

## 20. What Do SAST & DAST Scan?

* **SAST**: Static code vulnerabilities (e.g., SQL injection, XSS)
* **DAST**: Runtime flaws (e.g., broken auth, exposed endpoints)

## 21. How Did You Harden Docker Image?

* Use minimal base (e.g., `alpine`)
* Update base packages (`apt-get upgrade`)
* Remove compilers, docs, unnecessary tools

## 22. ACR, Kubernetes, Network Settings, Azure Storage

* ACR used as image registry
* AKS integrated via service principal or workload identity
* NSG & VNet integration
* Storage accounts with private endpoints

## 23. What Does Azure Migrate Offer?

* Server discovery & assessment
* App dependency mapping
* VM migration to Azure
* Database migration services

## 24. Do You Have Build / Unit Tests on PR?

* Yes, using **GitHub Actions / GitLab CI**
* PR triggers: Linting, Unit tests, Build validation

## 25. Idea on IIS & `.csproj` File

* IIS hosts ASP.NET apps
* `.csproj`: Project configuration file, includes dependencies, targets, output path

## 26. What to Define in `values.yaml`?

* Image tag
* Replica count
* Resource limits
* Environment-specific variables
* Ingress/Service config
* Secrets references

---

## 🧰 Tools & Platforms

* Azure (AKS, ACR, NSG, Storage, Azure Functions App)
* GitHub / GitLab
* Kubernetes
* Docker
* Ansible
* Helm
* Terraform
* Fortify (SAST/DAST)
* SonarQube, Trivy, BlackDuck, Twistlock
* Splunk, Prometheus, Grafana

---

Feel free to fork this repo and contribute enhancements or updates to questions via pull requests!

