## R720 Server / Setup and Configuration

This guide walks through the initial setup of a Dell PowerEdge R720xd, focusing on configuring **iDRAC** for remote management and install/config of **VMware ESXi**. 

The goal here is to get the server into a usable state with proper management access, RAID configured, and networking ready for virtualization. 

---

## Order of Operations

1. Enter **System Setup (F2)**  
2. Configure **BIOS Settings** (UEFI + boot order)  
3. Configure **iDRAC Settings** (set static IP)  
4. Verify **iDRAC connectivity** (ping + web login)  
5. Check **Device Settings** (NICs, disable VLAN mode)  
6. Reboot and enter **RAID Config (Ctrl+R)**  
7. Create and initialize **Virtual Disk Group**  
8. Install **ESXi**  
9. Configure **ESXi Management Network (F2)**  
10. Verify **ESXi connectivity** (ping + web login)  
11. Done!



---

### Boot-Time Options

| Hotkey    | Menu / Utility                                      |
|-----------|------------------------------------------------------|
| **F2**    | System Setup (BIOS/UEFI settings)                   |
| **F10**   | Lifecycle Controller (firmware, hardware config, OS) |
| **F11**   | Boot Manager (temporary boot device/order)           |
| **F12**   | PXE Boot (network boot)                              |
| **Ctrl+R**| PERC RAID Configuration Utility                      |
| **Ctrl+C**| HBA Configuration Utility (if applicable)            |
| **F5**    | System Diagnostics                                   |
| **Ctrl+E**| iDRAC Configuration Utility                          |

---

## Initial Setup

First, while booting, go into **System Setup (F2)** to configure iDRAC.  
We’re just going to setup the IP so we can reach it from a browser.  

![System Setup](/assets/SystemSetup.jpg)

### System BIOS
- Change **Boot Mode** to **UEFI**.  
- Change the **boot order** to load the disk you want to boot from.  
  - (In my case, I’m loading from an internal USB.)

### iDRAC Settings
- Go into **Network**.  
- Make sure all your NICs are **enabled**.  
- Set a **static IPv4 address, gateway, and mask**. 
![iDRAC Network](/assets/iDRACNetwork.jpg)


**Connectivity Check:** 
    After you assign the IP, go to another machine on the same network and **ping the iDRAC IP** to confirm it’s reachable.  

Later, you’ll log in via browser: `https://<iDRAC-IP>`.  


### Device Settings
- Under **Device Settings**, you’ll see *Integrated RAID Controller*.  
  - This is **NOT** where you configure disks/RAID.  
- Go into each NIC:  
  - Best left at default.  
  - Make sure all 4 are the same.  
  - **Disable VLAN mode** (unless you know exactly what you’re doing).  
  - They must match for load balancing.  
- VLAN tagging will be configured in **ESXi**, not iDRAC.  

---

## RAID Configuration

At this point, remove all but your drives (except your flash media, and the drive you want to install to). Then go ahead and install ESXi.  
(I won’t go over that here since it’s a pretty straightforward installation.)  

![RAID PERC](/assets/RAIDPERC.jpg)

- Reboot and hit **Ctrl+R** to configure RAID and disks.  
- You’ll see the classic *blue on blue* PERC interface.  

In the **Physical Disks** view, confirm it detects all drives.  
Then:  
- Highlight **Virtual Disk**  
- **F2** for Operations (see bottom of screen for controls)  
- Create a **virtual disk group**  
- Initialize it (**Fast Init** is fine).  

Note: I don’t believe there’s a clean “exit” option, so double-check everything and then reboot via the power button.  

---

## ESXi Configuration

After booting into ESXi:  
- **F2** to login to **System Customization**.  
- Go to **Configure Management Network** then **IPv4 Configuration**.  
- Set your management IPv4 address.  
- Then configure your VLAN.  

![ESXi Network](/assets/ESXiNetwork.jpg)

**Connectivity Check:**  
- From **Test Management Network** (inside ESXi), try pinging your gateway and DNS.  
- From another machine, ping the ESXi management IP to confirm it’s live.  

That’s really all we need to do here.

---
## Done!

At this point, you should be able to reach the web interfaces for both **iDRAC** and **ESXi** from another machine on the network.  

- iDRAC default login:  
  - **User:** root  
  - **Pass:** calvin  

![iDRAC Login](/assets/iDracLogIn.jpg)  
![ESXi Login](/assets/ESXiLogin.jpg)

