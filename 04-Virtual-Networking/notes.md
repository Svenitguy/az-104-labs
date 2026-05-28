# Lab 04 – Azure Virtual Networking (VNet, NSG, ASG, DNS)

## 📌 Overview
This lab demonstrates the design and implementation of a foundational Azure networking architecture.  
It focuses on network segmentation, security enforcement, and name resolution in a cloud environment.

---

# 🏗️ Task 1 – CoreServicesVnet Deployment

## 🎯 Objective
Deploy a Virtual Network with subnet segmentation to support scalable cloud workloads.

## 🛠️ Implementation
- Deployed Virtual Network: **CoreServicesVnet**
- Address space: `10.20.0.0/16`
- Created subnets:
  - SharedServicesSubnet → `10.20.10.0/24`
  - DatabaseSubnet → `10.20.20.0/24`
- Exported ARM template and parameters for Infrastructure as Code reuse

## 📸 Validation
- VNet successfully created in Azure Portal
- Subnets correctly assigned within address space
- ARM template export completed successfully

## 🧠 Key Learnings
- VNets provide isolated network boundaries in Azure
- Subnets enable workload segmentation and scalability
- Proper IP planning prevents future routing conflicts

---

# ⚙️ Task 2 – ManufacturingVnet via ARM Template

## 🎯 Objective
Deploy a second Virtual Network using Infrastructure as Code principles.

## 🛠️ Implementation
- Modified exported ARM template
- Deployed **ManufacturingVnet**
- Updated:
  - Address space: `10.30.0.0/16`
  - Subnets:
    - SensorSubnet1 → `10.30.20.0/24`
    - SensorSubnet2 → `10.30.21.0/24`

## 🔄 Changes Applied
- CoreServicesVnet → ManufacturingVnet
- 10.20.0.0 → 10.30.0.0
- SharedServicesSubnet → SensorSubnet1
- DatabaseSubnet → SensorSubnet2

## 📸 Validation
- ARM deployment succeeded
- ManufacturingVnet visible in Azure Portal
- Subnets correctly configured

## 🧠 Key Learnings
- ARM templates enable repeatable infrastructure deployment
- Parameterization improves maintainability
- Consistency in IP design is critical across environments

## 🌍 Real-World Relevance
This pattern is commonly used to deploy identical environments for:
- Development
- Testing
- Production

---

# 🔐 Task 3 – ASG & NSG Security Configuration

## 🎯 Objective
Implement network-level security using NSGs and ASGs.

## 🛠️ Implementation
- Created Application Security Group: **asg-web**
- Created Network Security Group: **myNSGSecure**
- Associated NSG with CoreServicesVnet subnet
- Configured security rules

## 🔒 Security Rules

### Inbound Rule
- Protocol: TCP
- Ports: 80, 443
- Source: Application Security Group (asg-web)
- Action: Allow
- Priority: 100

### Outbound Rule
- Destination: Internet (Service Tag)
- Action: Deny
- Priority: 4096

## 📸 Validation
- NSG successfully associated with subnet
- Rules visible and correctly applied
- Traffic filtering behavior verified

## 🧠 Key Learnings
- ASGs simplify dynamic workload security management
- NSGs enforce subnet-level traffic control
- Rule priority determines evaluation order (lower = higher priority)
- Azure uses default deny/allow system rules

## 🔐 Real-World Context
This design reflects a Zero Trust networking model where:
- Access is explicitly defined
- Outbound traffic is restricted
- Security is enforced at subnet boundary level

---

# 🌐 Task 4 – Azure DNS (Public & Private Zones)

## 🎯 Objective
Configure public and private DNS zones for external and internal name resolution.

---

## 🌍 Public DNS Zone

## 🛠️ Implementation
- Created public DNS zone
- Added A record: `www`
- Mapped hostname to IP address

## 📸 Validation
- DNS zone created successfully
- A record visible in Azure Portal
- nslookup confirmed successful resolution via Azure DNS

## 🧠 Key Learnings
- Public DNS enables external service name resolution
- Azure DNS provides authoritative name resolution services
- DNS delegation relies on name servers

---

## 🔒 Private DNS Zone

## 🛠️ Implementation
- Created private DNS zone: `private.contoso.com`
- Linked to **ManufacturingVnet**
- Created internal A record: `sensorvm`

## 📸 Validation
- Private DNS zone successfully created
- Virtual network link established
- Internal DNS record configured

## 🧠 Key Learnings
- Private DNS zones are scoped to VNets
- Enables internal service discovery without public exposure
- VNet linking is required for resolution

## 🌍 Real-World Relevance
- Public DNS: customer-facing applications
- Private DNS: internal microservices and backend systems
- Common in hybrid cloud architectures

---

# 🧠 Overall Key Takeaways

- Azure networking is built on isolation and segmentation principles
- Proper IP planning is essential for scalable architectures
- NSGs enforce stateful network security controls
- ASGs improve scalability of security rules
- DNS plays a critical role in service discovery across cloud environments
- Infrastructure as Code enables repeatable and consistent deployments

---

# 🚀 Conclusion

This lab demonstrates how core Azure networking components work together to form a secure and scalable cloud architecture. It provides foundational knowledge for advanced topics such as hybrid networking, routing, and enterprise-grade cloud design.