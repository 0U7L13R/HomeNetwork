# CorpoSec Network
*Corporate style home network & cyber range*

---

![alt text](assets/Front.jpg)
# Background
I initially bought a Raspberry Pi to start a small project running Pi-Hole while I was at University. After struggling to get it connected to Wi-Fi without a GUI, I glanced over at my unused Cisco gear and decided to start building out a network.

When my ambitions grew the Pi became obsolete, so I bought a dedicated server. I wanted to expand, host more services and even VMs. At this point I started to study for the CCNA.

My ambitions grew again, I wanted to model a corporate network, complete with a security stack, and a proper lab enviroment of VMs. So that I would learn the roles of analyst, engineer, and GRC.

---

## Documentation
- [Network Architecture](/docs/Network-Architecture.md) – Details network design and topology  
- [Services](/docs/Services.md) – Overview of applications hosted on the server  
- [SOC Stack](/docs/SOC.md) – Documentation of security tools, monitoring, and triage  
- [DevOps & Labs](/docs/DevOps-Lab.md) – Spinning VMs on ESXi and labs  
- [Server Setup](/docs/Server-Setup.md) – Installation steps, config, and deployment notes  
- /docs/
- /assets/

---
![alt text](assets/Full.jpg)
# Hardware
  - Dell Poweredge R720xd (ESXi on a Crucial BX500 SATA SSD)
  - Cisco Router
  - Cisco Switch
  - Cisco Access Point
  - Raspberry Pi 5
  
  **Rack**
  - StarTech 4-post 12U mobile open frame
  - 1U 19 inch Server Rack Rails (2)
  - 16 Outlet Horizontal 1U Rack Mount PDU
---
# Current State
- Network is up and running with VLANS, I still need to implement proper ACLs.
- Server is up and running as well, including iDRAC and such, and you can spin up and SSH into VMs.
- Raspberry Pi of course is no longer working. As I am transfering the apps I ran on it to the server.

I am currently focuing on getting my apps up and running.

---



