# Small Office Network Security Blueprint

## Project Overview
This project focuses on designing and securing a hypothetical small office network. The goal is to understand basic networking concepts, identify common security risks, and recommend appropriate security controls.

## Objectives
- Understand how a small office network is structured.
- Identify common networking devices and their functions.
- Develop an IP addressing plan.
- Understand network segmentation and access control.
- Identify potential cybersecurity risks.
- Recommend security measures to improve network protection.

## Tools & Technologies
- Cisco Packet Tracer
- Microsoft Excel
- GitHub
- Windows

## Project Scope
The simulated office environment will include:
- Employee computers
- Management workstation
- Network printer
- Internal server
- Router and network switch
- Employee and guest network concepts

## Planned Deliverables
- [ ] Network topology diagram
- [ ] Device inventory
- [ ] IP addressing plan
- [ ] Network segmentation design
- [ ] Security risk assessment
- [ ] Security recommendations
- [ ] Cisco Packet Tracer simulation
- [ ] Final project report

## Learning Outcomes
Through this project, I aim to develop practical knowledge of computer networking, network security, risk assessment, and technical documentation.

## Project Status
Currently in progress.

## Disclaimer
This project is designed for educational purposes using a hypothetical office environment. No unauthorized networks or systems will be accessed or tested.

---
**Author:** Samruddha Kale  
**Field:** IT & Cybersecurity
## Project Progress

### Milestone 1: Network Setup and VLAN Segmentation

- Created a small office network using a Cisco 1941 router and Cisco 2960 switch.
- Connected two PCs to separate VLANs.
- Created VLAN 10 (ADMIN) and VLAN 20 (EMPLOYEES).
- Configured an 802.1Q trunk between the switch and router.
- Configured router-on-a-stick for inter-VLAN routing.

### Milestone 2: ACL-Based Traffic Control

- Created an extended ACL named `EMPLOYEE-RESTRICTION`.
- Applied the ACL inbound on router subinterface `GigabitEthernet0/0.20`.
- Blocked IP traffic initiated from EMPLOYEES to ADMIN.
- Allowed ICMP echo replies from EMPLOYEES to ADMIN so ADMIN-initiated ping tests could succeed.

### Verification Results

| Test | Expected result | Actual result |
|---|---|---|
| PC0 → ADMIN gateway | Success | Passed |
| PC1 → EMPLOYEES gateway | Success | Passed |
| PC0 → PC1 before ACL | Success | Passed |
| PC1 → PC0 after ACL | Blocked | Passed |
| PC0 → PC1 after ACL | Success | Passed |
### Milestone 3: Network Hardening

- Configured switch port security on `Fa0/1` and `Fa0/2`.
- Set a maximum of one secure MAC address per access port.
- Enabled sticky MAC address learning.
- Configured violation mode as `restrict` to drop traffic from unauthorized MAC addresses while keeping the port active.
- Verified that both PC MAC addresses were learned as secure sticky addresses.
- Administratively disabled unused switch ports (`Fa0/3–Fa0/24` and `Gig0/2`).
- Kept active PC connections and the router uplink operational.

### Milestone 3 Verification Results

| Test | Expected result | Actual result |
|---|---|---|
| Port security on Fa0/1 and Fa0/2 | Enabled | Passed |
| Sticky MAC learning | One MAC per port | Passed |
| Unused FastEthernet ports | Disabled | Passed |
| Unused GigabitEthernet0/2 | Disabled | Passed |
| Active PC and router ports | Remain operational | Passed |
| PC0 → ADMIN gateway | Success | Passed |
| PC1 → EMPLOYEES gateway | Success | Passed |
| PC0 → PC1 | Success | Passed |

### Additional Security Notes

- Port security helps limit unauthorized device connections to access ports.
- Sticky MAC learning dynamically learns and stores secure MAC addresses.
- Restrict mode drops traffic from violating MAC addresses and records security violations.
- Unused switch ports are administratively disabled to reduce unnecessary access points.
### Security Notes

- VLANs provide logical network segmentation.
- Extended ACLs control traffic based on source and destination IP addresses and protocol.
- This is a basic stateless ACL demonstration, not a stateful firewall.
- Further security controls and testing are required before treating this as a production-ready network.
### Milestone 4: Secure Device Management

- Configured privileged EXEC password protection on the router.
- Created a local administrator account.
- Configured SSH version 2 for secure remote management.
- Disabled Telnet access on router VTY lines.
- Restricted router SSH management access to the ADMIN subnet using a standard ACL.
- Applied similar SSH-based management security to the switch.
- Verified remote SSH login to both SW1 and R1.
- Saved router and switch configurations.

### Milestone 4 Verification Results

| Test | Expected result | Actual result |
|---|---|---|
| Router SSH from ADMIN | Allowed | Passed |
| Switch SSH from ADMIN | Allowed | Passed |
| SSH management restriction | ADMIN subnet only | Configured |
| SSH version | Version 2 | Passed |
| Router configuration saved | Successful | Passed |
| ADMIN → EMPLOYEES | Allowed | Passed |
| EMPLOYEES → ADMIN | Blocked | Passed |

### Additional Security Notes

- SSH provides encrypted remote device management.
- Local user authentication avoids relying on a shared VTY password.
- The SSH management ACL limits remote access to the ADMIN subnet.
- RSA 1024-bit keys were used for Packet Tracer compatibility; production systems should use stronger supported key sizes.
- This project demonstrates basic network segmentation and access control, not a complete production security architecture.
