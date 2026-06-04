VM 105

OS: Ubuntu LTS 22.04
CPU 3 CPU(s)
Memory 4.00 GiB
Bootdisk size 20.00 GiB (Raid 1)

Pi-hole
Unbound installed natively 


This environment utilizes a self-hosted DNS stack combining Pi-hole and Unbound to manage name resolution and traffic filtering. Pi-hole serves as the central gateway for DNS queries, providing ad-blocking, local domain management, and visibility into client activity. Unbound operates as a recursive resolver, fetching records directly from root and TLD servers.

This architecture eliminates reliance on third-party DNS providers, enhances privacy by avoiding external logging, and simplifies internal service discovery through custom local records.

Design Objectives
The DNS layer was engineered to achieve the following:

Centralized Management: Unify DNS resolution for all local devices and hosted services under a single point of control.
Privacy & Security: Block malicious or unwanted domains at the network level and resolve queries recursively to prevent ISP tracking.
Internal Resolution: Enable seamless access to local services via custom hostnames rather than IP addresses.
Visibility: Gain granular insight into DNS query patterns across the entire network for troubleshooting and analysis.
Independence: Decouple internal infrastructure from public DNS dependencies to ensure consistent uptime and control.
Architecture Flow
The resolution path follows a strict chain of trust, ensuring queries are filtered before being resolved externally:


[ Client Device ]
       |
       v
[ Pi-hole ]  <-- Filters ads/malware, resolves local zones
       |
       v
[ Unbound ]  <-- Recursively queries root/TLD servers
       |
       v
[ Root / TLD / Authoritative Servers ]
By placing Pi-hole upstream of Unbound, the system ensures that all external traffic is vetted for threats and privacy leaks before leaving the local network, while still maintaining the speed and autonomy of recursive resolution.

