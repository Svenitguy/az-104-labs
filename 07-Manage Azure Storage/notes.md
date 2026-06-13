# Lab 07 – Azure Storage Notes

---

# 🏗️ Task 1 – Create and Configure Storage Account

## 🎯 Objective

Deploy a secure storage account using Geo-Redundant Storage (GRS).

## 🛠️ Implementation

Created:

* Storage account in East US
* Resource group: az104-rg7
* Redundancy: Geo-Redundant Storage (GRS)
* Public network access initially disabled, later restricted
* Lifecycle management rule (MoveToCool)

Enabled:

* Read access in case of regional failure

## 🧠 Key Learnings

* Azure Storage supports multiple redundancy models
* GRS provides disaster recovery capability
* Public access should be restricted by default
* Lifecycle management can automatically move data to lower-cost storage tiers

---

# 🧊 Task 2 – Secure Blob Storage

## 🎯 Objective

Create secure blob container and control access using RBAC + SAS.

## 🛠️ Implementation

### Blob Container

* Created container: `data`
* Access level: Private (no anonymous access)

### Upload

* Uploaded file to folder: `securitytest`
* Blob type: Block blob
* Access tier: Hot

### Access Control

* Public URL access → ❌ denied
* SAS token generated → ✅ allowed access
* RBAC role assigned:
  * Storage Blob Data Contributor

### Data Protection

* Time-based retention policy: 180 days
* Immutable blob storage enabled

## 🧠 Key Learnings

* Blob containers are private by default (best practice)
* SAS tokens provide temporary secure access
* RBAC is preferred for long-term identity-based access
* Immutable storage helps protect data against accidental deletion or modification

---

# 📁 Task 3 – Azure File Storage

## 🎯 Objective

Create and manage Azure File Shares.

## 🛠️ Implementation

### File Share

* Created: `share1`
* Access tier: Transaction optimized
* Backup: Disabled (lab simplification)

### Upload

* Uploaded file via Storage Browser
* Verified directory creation

### Access Method

* Azure Storage Browser used for management
* Authentication via Microsoft Entra ID

## 🧠 Key Learnings

* Azure Files supports SMB protocol
* Storage Browser simplifies file share management
* RBAC is required for secure access

---

# 🌐 Network Security Configuration

## 🎯 Objective

Restrict storage access to a virtual network.

## 🛠️ Implementation

* Created Virtual Network: `vnet1`
* Enabled Service Endpoint:
  * Microsoft.Storage
* Restricted access to:
  * Default subnet only
* Removed public IP access

## 🧠 Key Learnings

* * Service Endpoints allow secure access to Azure services over the Azure backbone network
* Storage accounts can be fully locked to VNets
* Public access should be removed in production environments

---

# 🧠 Overall Key Takeaways

* Storage accounts are the foundation of Azure data storage
* Blob storage is ideal for unstructured data
* Azure Files provides shared file system capabilities
* SAS tokens provide temporary secure access
* RBAC is the preferred authentication method
* Network restrictions significantly improve security
* Lifecycle policies help optimize storage costs
* Immutable storage improves data protection
* Service Endpoints enhance network security for Azure services

---

# 🚀 Conclusion

This lab demonstrates how Azure Storage can be securely configured for enterprise use.

It combines identity-based security, temporary access mechanisms, and network isolation to ensure data protection and controlled access.