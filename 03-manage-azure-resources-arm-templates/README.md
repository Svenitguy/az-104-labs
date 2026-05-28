# Lab 03 – Azure Resource Deployment Automation (ARM & Bicep)

## 🎯 Objective
Understand Infrastructure as Code (IaC) in Azure by deploying resources using ARM templates, PowerShell, CLI, and Bicep.

---

## 🧱 What I implemented
- Deployed Azure managed disks using multiple IaC methods:
  - Azure Portal export (ARM template)
  - Azure Resource Manager template redeployment
  - Azure PowerShell deployment
  - Azure CLI deployment
  - Bicep deployment

---

## 🧠 Key concepts learned
- Infrastructure as Code (IaC) enables repeatable and consistent deployments
- ARM templates are JSON-based declarative definitions of Azure resources
- Bicep is a cleaner abstraction over ARM templates
- PowerShell and CLI can both execute IaC deployments, depending on environment
- Cloud Shell provides a unified management environment

---

## 🔄 ARM vs Bicep (my understanding)
- ARM: verbose JSON, harder to read and maintain
- Bicep: cleaner syntax, modular, easier for scaling infrastructure
- Both compile to ARM internally

---

## ⚠️ Challenges / issues faced
- Parameter mismatches between template.json and parameters.json
- Switching Cloud Shell between PowerShell and Bash resets context
- Small syntax corrections required in Bicep file (SKU and disk size)
- Understanding deployment scopes (resource group level)

---

## 🚀 Real-world application
In production environments, these templates would:
- Be stored in a Git repository
- Be deployed using CI/CD pipelines (e.g. Azure DevOps or GitHub Actions)
- Follow version control and approval workflows
- Be reused across environments (dev/test/prod)

---

## 🧰 Tools used
- Azure Portal
- Azure Cloud Shell
- Azure CLI
- Azure PowerShell
- ARM Templates
- Bicep

---

## 📈 Key takeaway
This lab demonstrated how infrastructure automation reduces manual work and increases consistency across environments.

---

## 📌 Next step
Move to networking labs (VNets, NSGs) and start combining IaC with network architecture.