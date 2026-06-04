Network Infrastructure Design
Overview
This repository documents the network architecture supporting a self-hosted virtualization environment built on Proxmox VE. The design prioritizes reliable connectivity, secure remote access, and strict service segmentation across a mix of virtual machines and containers.

The network serves as the backbone for a diverse set of services, including DNS filtering, recursive resolution, media streaming, private cloud storage, centralized authentication, application hosting, and game server management.

Design Objectives
The architecture was built with several key goals in mind:

Performance: Deliver high-speed connectivity (10Gb internal) for core infrastructure and storage-heavy workloads.
Security: Minimize direct exposure of backend services by routing all external traffic through a reverse proxy and securing remote access via VPN.
Centralization: Consolidate DNS filtering and recursive resolution to simplify management and improve privacy.
Segmentation: Organize services by function to isolate failures and streamline administration.
Scalability: Create a flexible topology that can grow with new service requirements.
Core Components
Component	Role in Architecture
Fiber Internet	Primary WAN uplink for hosted services and remote connectivity
10Gb Internal Network	High-throughput backbone connecting the Proxmox host to storage and compute nodes
Proxmox VE	Central hypervisor hosting the entire service ecosystem
Pi-hole & Unbound	Combined DNS filtering and privacy-focused recursive resolution
WireGuard	Encrypted tunnel for secure remote access to the internal network
Traefik	Reverse proxy handling SSL termination, routing, and access control
Auth Services	Unified identity provider for centralized login across all protected services
High-Level Topology
The network follows a layered approach, moving from the public internet through security gateways to isolated service zones:


[ Internet ]
     |
[ Fiber Gateway / Router ]
     |
[ Multi-Gig / 10Gb Backbone ]
     |
[ Proxmox VE Host ]
     |
+-------------------------------------------------------+
|  DNS  |  Reverse Proxy  |  Auth  |  Media  | Storage |
+-------------------------------------------------------+
     |
[ Remote Access via WireGuard VPN ]
