## Network Topology

The network is designed using a **two-tier enterprise architecture** consisting of redundant edge routers, a highly available core layer, and multiple access layer switches serving end-user and data center networks.

### Edge Layer
- Two edge routers (**SpringR1** and **SpringR2**) provide redundant connectivity to separate upstream ISPs (simulated college networks).
- ISP-facing interfaces obtain IP addressing via DHCP, simulating a real-world service provider environment.
- The edge routers are interconnected using a point-to-point /30 network to enable routing synchronization and failover.

### Core Layer
- Two Layer 3 core switches (**SpringCoreR1** and **SpringCoreR2**) form the routing and switching backbone of the environment.
- Each core switch is redundantly connected to both edge routers using point-to-point /30 links.
- Dynamic routing is implemented using **OSPFv2 (single-area)** to ensure fast convergence and automatic failover.
- A first-hop redundancy protocol (FHRP) is used at the core layer to provide resilient default gateways for all VLANs.

### Access Layer
- Multiple access layer switches serve different floors and the data center:
  - Floor1-Acc1
  - Floor2-Acc3
  - Floor3-Acc3
  - Datacenter
- Each access switch is dual-homed to both core switches using **802.1Q trunk links**.
- Redundant uplinks are bundled using **EtherChannel** to increase bandwidth and provide link-level resiliency.
- Spanning Tree Protocol (RSTP) is tuned to prevent Layer 2 loops while ensuring rapid convergence.

### VLAN & Traffic Segmentation
- VLANs are used to logically separate tenant networks, management traffic, servers, and visitor access.
- Inter-VLAN routing is performed at the core layer, allowing centralized policy enforcement and access control.
- Trunk links between access and core switches carry only required VLANs to reduce unnecessary broadcast traffic.

### High Availability & Resilience
- Dual ISPs, redundant routers, redundant core switches, and dual-homed access switches eliminate single points of failure.
- Link failures, device failures, or ISP outages are handled through dynamic routing and gateway redundancy.
- The data center access switch is integrated into the same high-availability design to support critical services such as Active Directory, DNS, DHCP, IIS, and SQL Server.

This topology provides a **scalable, secure, and highly available foundation** suitable for a multi-tenant medical facility where uptime, segmentation, and security are critical.
