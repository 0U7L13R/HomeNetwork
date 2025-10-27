# Network Architecture

This document covers all networking related to the project, **except** for any networking with VMs running on the server.  


![Network Topology](/assets/Topology.jpg)
Switchport Config
![SwitchConfig](/assets/SwitchConfig.jpg)
---

## x.x.VLAN.x Schema

| VLAN ID | Name         | Notes                |
|---------|--------------|----------------------|
| 10      | Management   | ESXi / iDRAC         |
| 20      | Admin        |                      |
| 30      | Workstations |                      |
| 40      | Wireless     | Offline              |
| 50      | Printers     | Offline              |
| 60      | Cameras      | Offline              |
| 70      | Services     |                      |
| 80      | DevOps       |                      |
| 90      | SOC          | SIEM / Monitoring    |
| 100     | VPN          | DMZ                  |
| 110     | Guest        | DMZ                  |

---

## Sniffer Setup

The Dell R720 has 4 dedicated NIC ports.  
For packet analysis in the SOC, one port is reserved as a sniffer, while the other three are used for load balancing.  

### Steps
1. Configured NIC ports **1–3** as **trunk ports** with identical settings.  
   - (I orignally didn't think of this and had headaches on why I couldn't access ESXi)  
2. Reserved **NIC port 4** as the sniffer interface.  
   - Configured to receive a mirror/SPAN of all switch traffic.  
3. Unplugged the sniffer port during ESXi setup.  
4. In ESXi, created a **dedicated virtual switch** bound only to NIC port 4.  
5. Plugged NIC port 4 back in.  
   - The interface now listens passively to all mirrored traffic.  

---

