Network Topology
Overview
This network topology supports a self-hosted virtualization environment built on Proxmox VE. The infrastructure delivers secure remote access, centralized DNS,
reverse proxy routing, storage, authentication, media delivery, and game server hosting—all while maintaining reliability and scalability.

Enterprise hardware, high-speed networking, and virtualized services converge into a centralized platform capable of supporting diverse workloads and multiple users.

Infrastructure Overview

[ Internet ]
     |
[ 2.5 Gbps Fiber Connection ]
     |
[ Router / Gateway ]
     |
[ 2.5Gb / 10Gb Network ]
     |
[ Dell PowerEdge R730XD (Proxmox VE) ]
     |
+---------------------------------------------------+
|  DNS  |  Auth  |  Storage  |  Media  |  Games  |
+---------------------------------------------------+
Physical Infrastructure
Component	Specification
Server	Dell PowerEdge R730XD
CPU	2 × Intel Xeon E5-2697A v4
Memory	128 GB DDR4 ECC
Storage	22-drive enterprise storage array
Hypervisor	Proxmox VE 8
Boot Device	NVMe SSD
Networking	Mellanox ConnectX-4 10Gb
The server serves as the central virtualization host for all services.

Virtualization Layout
Services are isolated into dedicated virtual machines and containers based on function, security requirements, and resource demands.

Core Infrastructure Services
Proxmox VE
DNS Services
Authentication Services
Reverse Proxy Services
Storage Services
Application Services
Jellyfin Media Server
Nextcloud
Game Server Infrastructure
Containerized Applications
Monitoring and Administration Tools
This separation enables independent updates, maintenance, and security hardening for each service.

Network Services
DNS Infrastructure
DNS is handled through Pi-hole and Unbound, providing filtering, local DNS management, recursive resolution, and visibility into network activity.

Remote Access
Remote connectivity is secured via WireGuard VPN, allowing administrators and authorized users to access internal services without exposing management interfaces directly to the internet.

Reverse Proxy
External service access is managed through Traefik, which provides:

HTTPS encryption
SSL certificate management
Service routing
Access control integration
Storage Connectivity
The storage architecture supports both high-capacity and high-performance workloads through tiered storage pools:

Storage Type	Purpose
RAID6 SAS Array	Media and long-term storage
SSD Storage Pool	Virtual machine workloads
Shared Storage	Service data and application storage
This approach balances performance, redundancy, and scalability.

Service Relationships

[ Users ]
     |
[ WireGuard VPN / HTTPS ]
     |
[ Traefik Reverse Proxy ]
     |
+------------------------------------+
|  Auth  |  Media  |  Storage  |  Games  |
+------------------------------------+
           |
      [ DNS Services ]
           |
      [ Infrastructure ]
Security Design
Security is implemented through multiple layers:

VPN-based remote administration
Centralized authentication
HTTPS encryption
Internal service isolation
Dedicated service roles
Controlled external exposure
This layered approach minimizes unnecessary risk while maintaining accessibility for authorized users.

Scalability Considerations
The environment was designed with future expansion in mind. Key considerations include:

Additional virtual machines and containers
Storage expansion capability
Increased service workloads
Additional authentication integrations
Future monitoring and automation improvements
Lessons Learned
Designing and maintaining this environment provided practical experience in virtualization, storage planning, network architecture, service segmentation,
authentication integration, and infrastructure documentation. The project reinforced the importance of planning for growth, documenting changes, and designing systems 
that balance performance, security, and maintainability.
