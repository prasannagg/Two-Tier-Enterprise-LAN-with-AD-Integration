# Active Directory Integrated Two-Tier LAN Architecture  
**Spring Hill Medical Center – Enterprise Network & Systems Design**

## Overview
This project documents the planning, design, and implementation of a secure, highly available two-tier enterprise network and Windows systems infrastructure for a multi-tenant medical facility (Spring Hill Medical Center). The solution supports 10 tenant medical organizations and 150+ users while meeting security, availability, and scalability requirements typical of healthcare environments.

The project was completed as part of the CTN Program at Fanshawe College and simulates a real-world enterprise deployment using industry best practices.

---

## Business Scenario
Medic Networks is a medical infrastructure provider responsible for delivering centralized IT services to a multi-tenant medical building. The environment hosts multiple independent medical organizations that share centralized infrastructure while maintaining logical and administrative separation.

Key requirements included:
- Secure handling of sensitive medical data
- Network segmentation between tenants
- Centralized identity and access management
- High availability and fault tolerance
- Scalable addressing using IPv4 and IPv6

---

## Architecture Summary

### Network Architecture
- **Two-tier design** (Core & Access)
- Redundant edge connectivity to simulated ISPs
- Centralized data center services
- Visitor and tenant network isolation

**Key Technologies**
- VLAN-based segmentation
- Inter-VLAN routing on Layer 3 switches
- OSPFv2 (single-area) dynamic routing
- FHRP for default gateway redundancy
- EtherChannel for bandwidth aggregation and link redundancy
- Rapid Spanning Tree Protocol (RSTP)
- IPv4 / IPv6 dual-stack implementation
- NAT for Internet access

---

## Active Directory & Systems Design

### Forest & Domain Structure
- Forest root: `shmc.local` (Administrative domain)
- Child domain: `resources.shmc.local` (Resource domain)
- Alternate UPN suffixes per tenant organization
- Centralized identity with delegated administration

### Organizational Units & Delegation
- OU structure designed per tenant and department
- Delegated permissions for assistants to manage users and groups
- Separation of administrative, user, and resource objects
- Fine-grained administrative control without domain admin privileges

---

## Core Services Implemented

### Identity & Access
- Active Directory Domain Services (AD DS)
- Custom OU and Group Policy design
- Fine-Grained Password Policies
- Delegation of administration

### Network Services
- DHCP with scopes per VLAN
- DNS integrated with Active Directory
- IPv6 internal connectivity (no DHCPv6)
- Secure remote management via SSH

### Enterprise Applications
- IIS Web Server hosting internal application
- Microsoft SQL Server (separate DB server)
- Database-backed web application
- DNS name-based access (no IP-based access)

---

## High Availability & Redundancy
- Dual core switches with redundant uplinks
- EtherChannel between access and core layers
- FHRP for gateway failover
- OSPF routing convergence and failover
- STP tuning to prevent DHCP delays and loops

---

## Security Implementation

### Network Security
- Port security on access ports
- DHCP snooping to prevent rogue DHCP servers
- Trunk security and VLAN pruning
- ACLs to:
  - Restrict visitor access to internal resources
  - Allow only required services (DHCP, DNS, HTTP/HTTPS)
  - Restrict network device management to IT VLAN

### Systems Security
- Hardened server configurations
- Disabled unused services and ports
- Secure shared folders with role-based permissions
- Printer access controlled by security groups
- Administrator account hardening

---

## Network Management
- Centralized Syslog using Kiwi Syslog Server
- Configuration backups using SolarWinds TFTP Server
- Verified logging and backup/restore operations

---

## Verification & Testing
- OSPF neighbor adjacency and route validation
- VLAN and trunk verification
- DHCP lease assignment per VLAN
- AD replication and GPO application testing
- Web application and database connectivity testing
- ACL validation using controlled access tests

---

## Artifacts Included
- Network topology diagrams (Visio & PNG)
- CML canvas screenshots
- Addressing and VLAN design documentation
- Router and switch configuration files
- AD OU and GPO design documentation
- Verification screenshots and command outputs

---

## Skills Demonstrated
- Enterprise network design
- Routing & switching (CCNA-level and beyond)
- Windows Server & Active Directory administration
- Network security fundamentals
- Documentation and technical communication
- Troubleshooting and verification methodology

---

## Notes
Due to platform limitations, the original Cisco Modeling Labs (CML) YAML topology file is not included. Architecture, configuration logic, and verification are fully documented using diagrams, configuration files, and screenshots.

---

## Author
**Prasanna Koirala**  
Diploma – Computer & Network Technology  

