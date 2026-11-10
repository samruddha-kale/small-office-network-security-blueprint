# Small Office Network Security Blueprint

## 1. Introduction
This project focuses on designing and securing a hypothetical small office network using Cisco Packet Tracer. The main purpose is to understand how a small office network operates and how basic security measures can help protect network devices and internal resources.

The network consists of a Cisco 1941 router, a Cisco 2960 switch, and two end devices representing different departments. The network is divided into two VLANs: VLAN 10 (ADMIN) and VLAN 20 (EMPLOYEES), allowing logical network segmentation.

Router-on-a-stick configuration is used for inter-VLAN routing, while Access Control Lists (ACLs) are configured to restrict traffic between the two departments. Additional security measures include switch port security, disabling unused switch ports, and enabling SSH version 2 for secure remote device management.

The project is implemented and tested in a simulated environment using Cisco Packet Tracer. It demonstrates practical networking concepts, basic security configurations, and the importance of documenting and verifying network security controls.


## 2. Project Objectives
The main objectives of this project are:

1. To understand the basic structure and working of a small office network.
2. To identify the functions of routers, switches, and end devices.
3. To create an IP addressing plan for different network segments.
4. To implement VLAN-based network segmentation for ADMIN and EMPLOYEES.
5. To configure inter-VLAN routing using the router-on-a-stick method.
6. To implement Access Control Lists (ACLs) to control traffic between VLANs.
7. To improve network security using switch port security and unused-port shutdown.
8. To enable secure remote device management using SSH version 2.
9. To test network connectivity and verify the implemented security controls.
10. To document potential security risks, limitations, and recommendations.
    
## 3. Network Design
The small office network is designed using a Cisco 1941 router, a Cisco 2960 switch, and two end devices. The devices are connected using copper straight-through cables.

The router is connected to the switch through GigabitEthernet0/0 on the router and GigabitEthernet0/1 on the switch. The switch-to-router connection is configured as an 802.1Q trunk to carry traffic from multiple VLANs.

The two end devices are connected to separate access ports on the switch:

- PC0 is connected to FastEthernet0/1 and assigned to VLAN 10 (ADMIN).
- PC1 is connected to FastEthernet0/2 and assigned to VLAN 20 (EMPLOYEES).

### Logical Network Segmentation

The network is divided into two VLANs:

- VLAN 10 (ADMIN): Uses the subnet 192.168.10.0/24.
- VLAN 20 (EMPLOYEES): Uses the subnet 192.168.20.0/24.

### Inter-VLAN Routing

Router-on-a-stick is implemented on router R1 using two logical subinterfaces:

- GigabitEthernet0/0.10 handles VLAN 10 traffic.
- GigabitEthernet0/0.20 handles VLAN 20 traffic.

Each subinterface is assigned the corresponding VLAN gateway IP address. This allows communication between the VLANs, subject to the configured Access Control List.

### Network Topology Diagram

The network topology diagram illustrates the physical connections between the router, switch, and end devices, along with the two logical network segments.
![Small Office Network Topology](network-topology.png)

## 4. Device Inventory
The network consists of four devices: one router, one managed switch, and two end devices. Each device has a specific role in providing network connectivity, segmentation, and administration.

### 1. Router R1

- Model: Cisco 1941
- Role: Main network router.
- Interface connected to switch: GigabitEthernet0/0.
- Subinterfaces: GigabitEthernet0/0.10 and GigabitEthernet0/0.20.
- Responsibilities:
  - Provides inter-VLAN routing.
  - Acts as the default gateway for both VLANs.
  - Applies ACL-based traffic restrictions.
  - Supports secure remote management through SSH version 2.

### 2. Switch SW1

- Model: Cisco 2960.
- Role: Central network switch.
- Uplink: GigabitEthernet0/1.
- Connected end devices: PC0 and PC1.
- Responsibilities:
  - Provides VLAN-based network segmentation.
  - Connects the router and end devices.
  - Implements switch port security.
  - Disables unused switch ports.
  - Provides SSH-based remote management.

### 3. PC0 — ADMIN Workstation

- Device type: Packet Tracer PC.
- Connected interface: FastEthernet0/1 on SW1.
- VLAN: 10 (ADMIN).
- IP address: 192.168.10.10.
- Default gateway: 192.168.10.1.
- Purpose: Represents an administrative workstation.

### 4. PC1 — EMPLOYEES Workstation

- Device type: Packet Tracer PC.
- Connected interface: FastEthernet0/2 on SW1.
- VLAN: 20 (EMPLOYEES).
- IP address: 192.168.20.10.
- Default gateway: 192.168.20.1.
- Purpose: Represents an employee workstation.

## 5. IP Addressing Plan
The network uses private IPv4 addressing with a subnet mask of 255.255.255.0 (/24). Two separate subnets are configured to support the ADMIN and EMPLOYEES VLANs.

### IP Address Allocation

| Device | Interface | IP Address | Subnet Mask | Default Gateway | VLAN |
|---|---|---|---|---|---|
| R1 | G0/0.10 | 192.168.10.1 | 255.255.255.0 | N/A | 10 - ADMIN |
| R1 | G0/0.20 | 192.168.20.1 | 255.255.255.0 | N/A | 20 - EMPLOYEES |
| SW1 | VLAN 10 | 192.168.10.2 | 255.255.255.0 | 192.168.10.1 | 10 - ADMIN |
| PC0 | FastEthernet0 | 192.168.10.10 | 255.255.255.0 | 192.168.10.1 | 10 - ADMIN |
| PC1 | FastEthernet0 | 192.168.20.10 | 255.255.255.0 | 192.168.20.1 | 20 - EMPLOYEES |

### Subnet Details

**ADMIN Network**
- Network address: 192.168.10.0/24
- Default gateway: 192.168.10.1
- Subnet mask: 255.255.255.0
- Assigned VLAN: 10

**EMPLOYEES Network**
- Network address: 192.168.20.0/24
- Default gateway: 192.168.20.1
- Subnet mask: 255.255.255.0
- Assigned VLAN: 20

### IP Addressing Explanation

The router uses two logical subinterfaces, G0/0.10 and G0/0.20, to provide default gateway services to the respective VLANs.

The switch has a management IP address configured on its VLAN 10 interface. Its default gateway allows management traffic to reach devices outside its local subnet.

PC0 and PC1 use static IPv4 addressing. Each workstation is assigned an IP address from its respective subnet.

The addressing plan helps organise network devices and supports communication between the two VLANs through the router, subject to the configured ACL rules.

## 6. Security Implementation
The network implements multiple security controls to reduce unauthorized access and improve traffic management. These controls are configured on the Cisco 1941 router and Cisco 2960 switch.

### 6.1 VLAN-Based Network Segmentation

The switch is configured with two VLANs:

- VLAN 10 - ADMIN
- VLAN 20 - EMPLOYEES

PC0 is assigned to VLAN 10, while PC1 is assigned to VLAN 20.

This segmentation separates the two departments into different logical broadcast domains and provides a foundation for applying network access restrictions.

### 6.2 Router-on-a-Stick Configuration

Inter-VLAN routing is implemented using router R1.

The physical interface GigabitEthernet0/0 is configured with two logical subinterfaces:

- G0/0.10 for VLAN 10.
- G0/0.20 for VLAN 20.

The connection between SW1 and R1 is configured as an 802.1Q trunk, allowing both VLANs to communicate through the router when permitted by the configured access control rules.

### 6.3 ACL-Based Traffic Control

An extended Access Control List named EMPLOYEE-RESTRICTION is configured on router R1.

The ACL is applied inbound on GigabitEthernet0/0.20.

Its rules are:

- Permit ICMP echo-reply traffic from the EMPLOYEES subnet to the ADMIN subnet.
- Deny other IP traffic from the EMPLOYEES subnet to the ADMIN subnet.
- Permit other IP traffic.

This configuration restricts employee-initiated traffic towards the ADMIN network while allowing the specified ICMP echo-reply exception.

### 6.4 Switch Port Security

Port security is configured on the following switch interfaces:

- FastEthernet0/1
- FastEthernet0/2

The configuration includes:

- Maximum of one secure MAC address per port.
- Sticky MAC address learning.
- Restrict violation mode.

This helps limit unauthorized device connections through the configured access ports.

### 6.5 Disabling Unused Switch Ports

Unused switch interfaces are administratively disabled.

The following interfaces are shut down:

- FastEthernet0/3 through FastEthernet0/24.
- GigabitEthernet0/2.

The active PC connections and router uplink remain operational.

This reduces unnecessary physical network access points.

### 6.6 Secure Device Management Using SSH

SSH version 2 is configured on both R1 and SW1.

The management configuration includes:

- Local username authentication.
- Enable secret configuration.
- SSH version 2.
- Telnet access disabled on the configured VTY lines.
- RSA key generation for SSH.

An additional standard ACL named SSH-ADMIN-ONLY is configured on R1's VTY lines to permit SSH management access from the ADMIN subnet and deny other source addresses.

SSH access was successfully tested from PC0 to both network devices.

## 7. Testing and Verification
The network was tested using ping commands, SSH login attempts, and Cisco IOS verification commands. These tests were performed in Cisco Packet Tracer to confirm connectivity and verify the configured security controls.

### 7.1 Connectivity Testing

| Test | Expected Result | Actual Result |
|---|---|---|
| PC0 to ADMIN gateway (192.168.10.1) | Successful | Successful |
| PC1 to EMPLOYEES gateway (192.168.20.1) | Successful | Successful |
| PC0 to PC1 (192.168.20.10) | Successful | Successful |
| PC1 to PC0 (192.168.10.10) | Blocked by ACL | Blocked |
| R1 to PC1 | Successful | Successful |
| PC0 to SW1 management IP (192.168.10.2) | Successful | Successful |

### 7.2 ACL Verification

The EMPLOYEE-RESTRICTION ACL was checked using the `show access-lists` command.

The test confirmed that traffic initiated from the EMPLOYEES network towards the ADMIN network was blocked, while the permitted traffic rules remained in place.

### 7.3 Port Security Verification

Port security was checked on switch interfaces Fa0/1 and Fa0/2.

The verification confirmed:
- Port security was enabled.
- Maximum secure MAC addresses were set to one per port.
- Sticky MAC address learning was configured.
- Violation mode was set to restrict.

### 7.4 SSH Verification

SSH version 2 was verified on both R1 and SW1.

SSH login from the ADMIN workstation (PC0) to both network devices was successful. The VTY lines were configured to accept SSH rather than Telnet.

### 7.5 Overall Test Result

The tests confirmed that the network provided the intended VLAN separation, inter-VLAN traffic control, switch port security, and secure remote device management within the Packet Tracer simulation.

## 8. Security Risk Assessment
This section identifies potential security risks in the hypothetical small office network and evaluates their possible impact. The assessment considers the network design, configured security controls, and limitations of the Packet Tracer simulation.

| Security Risk | Possible Impact | Existing Mitigation |
|---|---|---|
| Unauthorized access between network segments | Employees may access sensitive ADMIN resources | VLAN segmentation and ACL restrictions |
| Unauthorized device connection | An unknown device may connect through a switch port | Port security with sticky MAC learning |
| Unauthorized remote management access | Attackers may attempt to manage network devices | SSH v2, local authentication, and VTY access restrictions |
| Unused switch ports being accessed | Unused connections could be misused | Unused switch ports are administratively shut down |
| Weak device passwords | Unauthorized users may gain administrative access | Local authentication and enable secrets; strong unique passwords are recommended |
| Misconfiguration of network devices | Incorrect settings may weaken network security or disrupt connectivity | Configuration verification and documentation |
| Lack of network monitoring | Suspicious activity may go unnoticed | Monitoring and logging are recommended for future implementation |

### Risk Assessment Summary

The implemented controls reduce several common risks, including unauthorized inter-VLAN communication, unauthorized device connections, and insecure remote device management.

However, the network still has limitations. The ACL is stateless, and the simulation does not include advanced monitoring, intrusion detection, centralized logging, or redundant network devices.

These risks should be considered when expanding the design for a real office environment.

## 9. Security Recommendations
The following recommendations could further improve the security of the small office network. These measures are suggested for future implementation and are not all currently configured in the Packet Tracer simulation.

### 9.1 Strong Authentication

Use strong, unique passwords for router and switch administration. Where supported, implement multi-factor authentication for administrative access.

### 9.2 Stronger SSH Encryption

Use stronger RSA key sizes, such as 2048 bits or higher, where supported by the device. The current Packet Tracer configuration uses a 1024-bit RSA key for compatibility.

### 9.3 Network Monitoring and Logging

Implement centralized logging and network monitoring to help administrators identify unusual activity, configuration changes, and possible security incidents.

### 9.4 Firewall Protection

Deploy a suitable firewall with stateful inspection to provide more advanced traffic filtering and protection between internal networks and external networks.

### 9.5 Regular Configuration Backups

Maintain secure backups of router and switch configurations. Review backups periodically to ensure that configurations can be restored when required.

### 9.6 Firmware and Software Updates

Keep network device firmware and software updated to address known vulnerabilities and improve security.

### 9.7 Network Redundancy

Consider additional network devices and backup connectivity to reduce downtime if a device or connection fails.

### Recommendation Summary

Implementing these measures would improve the security, reliability, and maintainability of the network if the design were expanded for a real office environment.

## 10. Project Limitations

## 11. Conclusion
