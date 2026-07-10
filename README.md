# 🔐 DevBoard – End-to-End DevSecOps CI/CD Pipeline

A production-grade **DevSecOps CI/CD pipeline** implementing **automated code quality checks, security scanning, container validation, and secure deployment** using GitHub Actions.

This project demonstrates a **complete Shift-Left + Shift-Right security approach** with **PR-based validation, modular CI workflows, and event-driven CD pipeline**.

---

## 🚀 Key Highlights

* 🔄 PR-based automated validation pipeline
* 🔐 Integrated DevSecOps (SAST, Dependency Scan, Secret Scan, DAST)
* 🐳 Docker linting, build & push automation
* ⚡ Modular reusable GitHub Actions workflows
* 🚀 Event-driven CD using `workflow_run`
* 🛡️ OWASP ZAP runtime security testing

---

## 🏗️ Pipeline Architecture

```text
Pull Request → CI Checks → Merge (CI) → Deploy → DAST Scan
```

---

## 🧪 PR Pipeline – `PR-pipeline-checks`

Triggered on:

```yaml
pull_request:
  branches: [master]
  types: [opened, synchronize]
```

### 🔹 Checks Performed

✔ **Frontend Code Quality**

* Node.js linting & validation

✔ **Backend Code Quality**

* Go code checks & dependency validation

✔ **Secret Scanning**

* Detects hardcoded secrets

✔ **Dependency Security Check**

* Vulnerability scanning for frontend & backend

✔ **Docker Lint & Scan**

* Validates Dockerfiles
* Ensures secure image build practices

---

### 💬 PR Automation

After all checks pass, an automated comment is added:

> **All CI Checks Completed Successfully**
> This pull request meets quality and security standards and is ready for review.

---

## ⚙️ CI Pipeline – `merge` Workflow

Triggered on:

```yaml
push:
  branches: [master]
```

### 🔹 Jobs

#### 1. SonarQube Scan (SAST)

* Runs static code analysis
* Ensures code quality & maintainability

#### 2. Docker Build & Push

* Builds frontend & backend images
* Pushes images to Docker Hub

---

## 🚀 CD Pipeline – `Devsecops-deploy.yml`

Triggered via:

```yaml
workflow_run:
  workflows: [merge]
  types: completed
```

### 🔹 Jobs

✔ **Deploy Application**

* Uses reusable deployment workflow

✔ **OWASP ZAP Scan (DAST)**

* Runs after deployment
* Performs runtime vulnerability testing

---

## 🔐 DevSecOps Coverage

| Stage        | Security Implementation            |
| ------------ | ---------------------------------- |
| PR Stage     | SAST, Secret Scan, Dependency Scan |
| Build Stage  | Docker Lint & Secure Build         |
| CI Stage     | SonarQube Analysis                 |
| Deploy Stage | Controlled Deployment              |
| Runtime      | OWASP ZAP (DAST)                   |

---

## 📂 Repository Structure

```bash
.
├── .github/workflows/
│   ├── PR-pipeline-checks.yml
│   ├── merge.yml
│   ├── Devsecops-deploy.yml
│   ├── Node-code-quality.yml
│   ├── Go-code-quality.yml
│   ├── secret-scanning.yml
│   ├── security-check.yml
│   ├── docker-lint.yml
│   ├── Sonarcube.yml
│   ├── docker-push.yml
│   ├── deploy.yml
│   ├── OWASP_DAST.yml
│
├── frontend/
├── backend/
└── README.md
```

---

## 🔄 Workflow Design

This project follows modern DevOps best practices:

* ✅ Shift-Left Security (PR validation)
* ✅ Reusable workflows for modular design
* ✅ CI/CD separation
* ✅ Event-driven pipeline chaining
* ✅ Automated PR feedback

---

## 🚀 Getting Started

### 1️⃣ Clone Repository

```bash
git clone https://github.com/rohit5126/devboard-cicd-secure-delivery.git
cd devboard-cicd-secure-delivery
```

---

### 2️⃣ Configure Secrets & Variables

#### 🔐 Secrets

* `SONAR_TOKEN`
* `DOCKER_TOKEN`

#### ⚙️ Variables

* `SONAR_HOST_URL`
* `DOCKER_USER`

---

### 3️⃣ Trigger Pipelines

* Create PR → triggers **PR pipeline checks**
* Merge → triggers **CI pipeline**
* CI completion → triggers **CD pipeline automatically**

---

## 📊 Key Features

✔ Full DevSecOps pipeline implementation
✔ Automated PR validation & feedback
✔ Multi-layer security checks
✔ Docker-based build system
✔ Real-world CI/CD architecture

---


## 🔮 Future Enhancements

* ☸️ Kubernetes deployment (Helm)
* 📊 Monitoring (Prometheus + Grafana)
* 🔐 Secrets management (Vault)
* 🏗️ Infrastructure as Code (Terraform)

---

## 🤝 Contributing

Feel free to fork and enhance this pipeline with more tools or improvements.

---

⭐ **Star this repo if you found it useful!**
