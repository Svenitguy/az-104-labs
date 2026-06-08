# Lab 06 – Azure Network Traffic Management Notes

## 📌 Overview

This lab demonstrates how Azure provides traffic management at both the network and application layers using Azure Load Balancer and Azure Application Gateway.

It focuses on how incoming client traffic is distributed across backend resources, how backend health is continuously monitored, and how routing decisions differ between Layer 4 and Layer 7 services.

---

# 🏗️ Task 1 – Deploy Lab Infrastructure

## 🎯 Objective

Deploy the lab environment using an ARM template.

## 🛠️ Implementation

Resources deployed:

* Virtual Network
* Network Security Group
* Three Virtual Machines

Environment:

* az104-06-vnet1
* az104-06-vm0
* az104-06-vm1
* az104-06-vm2

## 📸 Validation

* Deployment completed successfully
* All resources created
* VMs accessible

## 🧠 Key Learnings

* ARM templates provide repeatable deployments
* Infrastructure can be deployed consistently using declarative configuration
* Azure Resource Manager manages dependencies automatically

---

# ⚖️ Task 2 – Configure Azure Load Balancer

## 🎯 Objective

Distribute incoming TCP traffic across backend virtual machines.

## 🛠️ Implementation

Created:

### Frontend Configuration

* Public IP Address
* az104-fe

### Backend Pool

* az104-be
* az104-06-vm0
* az104-06-vm1

### Health Probe

* Protocol: TCP
* Port: 80

### Load Balancing Rule

* Frontend Port: 80
* Backend Port: 80

## 📸 Validation

Observed:

```text
Hello World from az104-06-vm0
```

and

```text
Hello World from az104-06-vm1
```

when refreshing the browser.

## 🧠 Key Learnings

* Azure Load Balancer operates at Layer 4
* Health probes determine backend availability
* Only healthy servers receive traffic
* Backend pools simplify resource management

---

# 🌐 Task 3 – Configure Azure Application Gateway

## 🎯 Objective

Route HTTP/HTTPS traffic based on URL path patterns.

## 🛠️ Implementation

Created:

### Dedicated Subnet

```text
subnet-appgw
```

### Application Gateway

```text
az104-appgw
```

### Backend Pools

```text
az104-appgwbe
```

```text
az104-imagebe
```

```text
az104-videobe
```

### Routing Rules

```text
/image/*
```

→ Image Backend

```text
/video/*
```

→ Video Backend

## 📸 Validation

Verified:

```text
http://<public-ip>/image/
```

redirected to image backend.

Verified:

```text
http://<public-ip>/video/
```

redirected to video backend.

Backend Health:

```text
Healthy
```

for all configured targets.

## 🧠 Key Learnings

* Application Gateway operates at Layer 7
* URL paths can be used for routing decisions
* Application Gateway understands HTTP traffic
* Backend health monitoring improves reliability

---

# 📚 Networking Concepts Learned

## Azure Load Balancer

Provides Layer 4 traffic distribution.

Routing decisions are based on:

* Source IP
* Destination IP
* Protocol
* Port

Cannot inspect HTTP requests.

---

## Azure Application Gateway

Provides Layer 7 traffic management.

Supports:

* Path-based routing
* Host-based routing
* SSL termination
* Web Application Firewall

Can inspect HTTP and HTTPS traffic.

---

## Health Probes

Used to continuously monitor backend health and availability.

Benefits:

* Fault detection
* High availability
* Automatic failover

---

## Backend Pools

Logical grouping of backend resources.

Benefits:

* Simplified management
* Scalability
* Centralized traffic distribution

---

# 🧠 Overall Key Takeaways

* Azure Load Balancer operates at Layer 4
* Azure Application Gateway operates at Layer 7
* Health probes ensure traffic is sent only to healthy resources
* Backend pools simplify traffic distribution
* Path-based routing enables application-aware traffic management
* Application Gateway provides advanced web traffic control

---

# 🚀 Conclusion

This lab provided practical experience with Azure traffic management technologies.

The concepts learned form the foundation for high availability architectures, web application delivery, reverse proxy solutions, and enterprise-scale Azure networking environments.
