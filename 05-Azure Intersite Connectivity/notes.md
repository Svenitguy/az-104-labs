# Lab 05 – Azure Intersite Connectivity Notes

## 📌 Overview

This lab focuses on enabling communication between isolated Azure Virtual Networks using VNet Peering and validating connectivity with Azure networking tools.

Additional routing control is implemented using User Defined Routes (UDRs) and Route Tables.

---

# 🏗️ Task 1 – Deploy Core Services Environment

## 🎯 Objective

Create a virtual machine within a dedicated virtual network representing shared IT infrastructure.

## 🛠️ Implementation

### Virtual Network

* Name: CoreServicesVnet
* Address Space: `10.0.0.0/16`

### Subnet

* Core → `10.0.0.0/24`

### Virtual Machine

* Name: CoreServicesVM
* OS: Windows Server 2025 Datacenter
* Size: Standard_D2s_v3

## 📸 Validation

* VM deployed successfully
* Private IP assigned
* VNet and subnet visible in Azure Portal

## 🧠 Key Learnings

* Azure automatically creates system routes
* VM network interfaces are attached to subnets
* VNets provide logical isolation boundaries

---

# 🏭 Task 2 – Deploy Manufacturing Environment

## 🎯 Objective

Deploy a second isolated network environment.

## 🛠️ Implementation

### Virtual Network

* Name: ManufacturingVnet
* Address Space: `172.16.0.0/16`

### Subnet

* Manufacturing → `172.16.0.0/24`

### Virtual Machine

* Name: ManufacturingVM
* OS: Windows Server 2025 Datacenter

## 📸 Validation

* Deployment completed successfully
* VM assigned private IP
* VNet visible in Azure Portal

## 🧠 Key Learnings

* Different address spaces are required
* Overlapping networks would prevent peering

---

# 🔍 Task 3 – Network Watcher Connectivity Testing

## 🎯 Objective

Verify communication between isolated virtual networks.

## 🛠️ Implementation

Used Azure Network Watcher:

* Source VM: CoreServicesVM
* Destination VM: ManufacturingVM
* Protocol: TCP
* Port: 3389

## 📸 Validation

Result:

```text
Connectivity Status: Unreachable
```

## 🧠 Key Learnings

* VNets are isolated by default
* No communication exists without explicit connectivity configuration
* Network Watcher simplifies troubleshooting

---

# 🔗 Task 4 – Configure VNet Peering

## 🎯 Objective

Enable private communication between both virtual networks.

## 🛠️ Implementation

Created bidirectional peering:

### CoreServicesVnet

* CoreServicesVnet-to-ManufacturingVnet

### ManufacturingVnet

* ManufacturingVnet-to-CoreServicesVnet

Enabled:

* Virtual network access
* Forwarded traffic

## 📸 Validation

Peering Status:

```text
Connected
```

for both virtual networks.

## 🧠 Key Learnings

* Peering uses Azure backbone networking
* Communication remains private
* No VPN Gateway required
* VNet Peering operates over Azure’s private backbone and does not require public IPs or gateways.

---

# 🧪 Task 5 – PowerShell Connectivity Validation

## 🎯 Objective

Verify connectivity after peering configuration.

## 🛠️ Implementation

Enabled Remote Desktop firewall rules:

```powershell
Enable-NetFirewallRule -DisplayGroup "Remote Desktop"
```

Tested connectivity:

```powershell
Test-NetConnection <CoreServicesVM-IP> -Port 3389
```

## 📸 Validation

Result:

```text
TcpTestSucceeded : True
```

## 🧠 Key Learnings

* Network connectivity in Azure is multi-layered and depends on:
  * Network layer (VNet Peering and routing)
  * OS layer (Windows Firewall)
  * Port-level access (TCP 3389 in this case)

* VNet Peering alone does not guarantee end-to-end connectivity, as traffic can still be blocked at the operating system or firewall layer.
---

# 🛣️ Task 6 – User Defined Routes (UDR)

## 🎯 Objective

Control traffic flow using custom routing.

## 🛠️ Implementation

### Perimeter Subnet

```text
10.0.1.0/24
```

### Route Table

```text
rt-CoreServices
```

### Custom Route

Destination:

```text
10.0.0.0/16
```

Next Hop Type:

```text
Virtual Appliance
```

Next Hop:

```text
10.0.1.7
```

Associated route table with:

```text
Perimeter Subnet
```

## 📸 Validation

* Route created successfully
* Route table associated with subnet

## 🧠 Key Learnings

* User Defined Routes (UDRs) override Azure system routes at subnet level, enabling controlled traffic flow through network appliances such as NVAs or firewalls.
* Route tables are associated with subnets and influence traffic direction for all resources within that subnet.
* UDRs are commonly used in enterprise architectures for traffic engineering, forced tunneling, and centralized security inspection (e.g., Azure Firewall or NVAs).

---

# 📚 Networking Concepts Learned

## VNet Peering

Provides private communication between Azure virtual networks using Microsoft's backbone infrastructure.

Benefits:

* Low latency
* High bandwidth
* No internet exposure

---

## Network Watcher

Azure diagnostic service used for:

* Connectivity testing
* Packet capture
* Topology visualization
* Route troubleshooting

---

## User Defined Routes (UDR)

Custom routes that override Azure default routing decisions.

Common uses:

* Forced tunneling
* Security inspection
* Centralized firewall architectures

---

# 🧠 Overall Key Takeaways

* Azure VNets are isolated by default
* VNet Peering enables secure private connectivity
* Network Watcher is valuable for troubleshooting
* Connectivity depends on routing and firewall configuration
* User Defined Routes provide granular traffic control
* Route tables are applied to subnets, not virtual machines

---

# 🚀 Conclusion

This lab provided practical experience with Azure network connectivity, troubleshooting, and routing.

The concepts learned in this lab form the foundation for more advanced architectures such as Hub-and-Spoke networking, Azure Firewall deployments, VPN Gateway connectivity, and enterprise hybrid cloud environments.
