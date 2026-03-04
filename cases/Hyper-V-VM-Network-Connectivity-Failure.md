# Hyper-V VM Network Connectivity Failure (APIPA Address) — Troubleshooting

## Overview

During the deployment of a **Windows Server 2022 Domain Controller lab in Hyper-V**, the virtual machine failed to obtain network connectivity. The VM automatically assigned itself an **APIPA address (169.254.x.x)**, preventing communication with the local router and blocking further configuration steps such as installing Active Directory Domain Services.

This case study documents the troubleshooting process used to diagnose and resolve the issue.

---

# Environment

| Component | Details |
|---|---|
| Hypervisor | Microsoft Hyper-V |
| Host OS | Windows 11 |
| VM OS | Windows Server 2022 |
| Network Adapter | Intel Wi-Fi 6 AX200 |
| Router Network | 192.168.50.0/24 |
| Hyper-V Switch Type | External Virtual Switch |

---

# Problem Description

- After installing Windows Server in Hyper-V and attempting to configure networking, the VM showed the following output:  

```
ipconfig 
```
Ethernet adapter Ethernet:

Autoconfiguration IPv4 Address: 169.254.44.244
Subnet Mask: 255.255.0.0
Default Gateway: 192.168.50.1  

- Attempts to renew DHCP failed:
```
ipconfig /renew
```
Output:


The operation failed as no adapter is in the state permissible for this operation.  

- Attempted ping:
```
ping 192.168.50.1
```  
Result:

Request timed out
Destination host unreachable  


---

# Initial Diagnosis

The **169.254.x.x address range** indicates **APIPA (Automatic Private IP Addressing)**.

APIPA occurs when:

- A device cannot contact a **DHCP server**
- The network adapter is **not connected to a working network**
- The virtual switch or bridge configuration is incorrect

Because the router should provide DHCP, this suggested a **Hyper-V networking issue**.

---

# Troubleshooting Steps

## 1. Verified Virtual Switch Configuration

1. Checked the VM network adapter settings in **Hyper-V Manager** 

2. Confirmed the switch was bound to the host’s physical adapter
Recreated Hyper-V External Switch

3. Because Wi-Fi bridging with Hyper-V can occasionally fail during initialization, the external switch was recreated.  

4. The VM network adapter was then reattached to the recreated switch.


5. Implemented Manual Static IP

Since DHCP renewal continued to fail, a manual IP configuration was applied.

Network settings configured:  
IP Address: 192.168.50.10
Subnet Mask: 255.255.255.0
Default Gateway: 192.168.50.1
Preferred DNS: 8.8.8.8  


This restored network connectivity.

---

# Verification

Connectivity was verified using:
```
ping 192.168.50.1
```
Successful replies confirming internet connectivity


---

# Root Cause

The issue was caused by **Hyper-V external switch DHCP traffic failing to pass through the Wi-Fi adapter**, resulting in the VM being unable to reach the DHCP server.

This caused Windows to assign an **APIPA address (169.254.x.x)**.

---

# Resolution

The issue was resolved by:

1. Recreating the Hyper-V external virtual switch.
2. Assigning a manual static IP configuration within the VM.

Once connectivity was confirmed, the server could proceed with **Active Directory installation and domain controller promotion**.

---

# Key Lessons Learned

- APIPA addresses indicate **DHCP failure**, not necessarily NIC failure.
- Hyper-V networking over Wi-Fi can be less reliable than Ethernet bridging.
- Manual IP assignment is an effective workaround in lab environments.
- Network connectivity should always be verified before installing Active Directory services.

---

# Related Lab

This troubleshooting occurred during the setup of:  
Active Directory Help Desk Lab  
Windows Server 2022 Domain Controller  
Domain: lab.local  

