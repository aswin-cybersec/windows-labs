# Windows Troubleshooting Lab

## Objective
Perform end-to-end network connectivity verification between 
Windows 10 and Kali Linux VMs using ICMP ping across a 
VirtualBox NAT Network.

## Environment
- Host OS: Windows 11
- VM 1: Windows 10 (VirtualBox)
- VM 2: Kali Linux (VirtualBox)
- Network: VirtualBox NAT Network (10.0.2.0/24)

## Tools Used
- VirtualBox
- Windows Command Prompt
- Kali Linux Terminal
- ICMP Ping

## Network Configuration
| Machine    | IP Address  | Gateway   |
|------------|-------------|-----------|
| Windows 10 | 10.0.2.3    | 10.0.2.1  |
| Kali Linux | 10.0.2.15   | 10.0.2.1  |

## Troubleshooting Methodology
1. Loopback test - 127.0.0.1
2. LAN connectivity - ping between VMs
3. Gateway test - ping 10.0.2.1
4. Internet connectivity - ping 8.8.8.8

## Results
| Test | From | Target | Result |
|------|------|--------|--------|
| Loopback | Windows 10 | 127.0.0.1 | ✅ Pass |
| Loopback | Kali Linux | 127.0.0.1 | ✅ Pass |
| LAN | Windows 10 | 10.0.2.15 | ✅ Pass |
| LAN | Kali Linux | 10.0.2.3 | ✅ Pass |
| Gateway | Windows 10 | 10.0.2.1 | ✅ Pass |
| Gateway | Kali Linux | 10.0.2.1 | ✅ Pass |
| Internet | Windows 10 | 8.8.8.8 | ✅ Pass |
| Internet | Kali Linux | 8.8.8.8 | ✅ Pass |

## Key Findings
- Windows Firewall blocks ICMP by default. 
  Added inbound rule to allow ICMPv4.
- TTL values identify device type:
  64 = Linux, 128 = Windows, 255 = Network device
- Both VMs confirmed full connectivity: 
  loopback → LAN → gateway → internet

## Lessons Learned
- Ping failure does not always mean the device is offline.
  Firewall rules can silently drop ICMP packets.
- NAT mode isolates VMs. NAT Network mode allows 
  inter-VM communication.
- The 4-step ping sequence is the standard first response 
  to any connectivity complaint in IT Support.

---
## Lab 2 - Windows System Diagnostics

### Objective
Perform Windows system diagnostics using built-in 
tools to simulate real IT Support troubleshooting tasks.

### Tools Used
- Command Prompt (Admin)
- Event Viewer
- Services.msc
- Task Manager
- System File Checker (SFC)

### Steps Performed

| Step | Command/Tool | Finding |
|------|-------------|---------|
| 1 | ipconfig /all | DHCP enabled, DNS: ISP servers |
| 2 | systeminfo | Windows 10 Home, 2GB RAM, 5 hotfixes |
| 3 | Event Viewer | Event ID 7000 - WdiServiceHost failed to start |
| 4 | Services.msc | Restarted Windows Update service successfully |
| 5 | Task Manager | High CPU - Windows Update running in background |
| 6 | sfc /scannow | Found and repaired corrupt system files |

### Key Findings
- Event ID 7000 = Service failed to start (permissions issue)
- High CPU at idle caused by Windows Update background activity
- sfc /scannow found and repaired corrupt files on fresh install
- Normal behavior on new VM — not a critical issue

### Lessons Learned
- Always check Task Manager before assuming hardware failure
- sfc /scannow is first response to system instability complaints
- High CPU does not always mean malware — check Windows Update first
- Event Viewer is the primary log source for Windows diagnostics
---

## Lab 3 - DNS Troubleshooting

### Objective
Understand DNS resolution, simulate a DNS failure, 
and fix it using Windows built-in tools.

### Tools Used
- Command Prompt
- nslookup
- ipconfig /flushdns
- ipconfig /displaydns
- Network Adapter Settings (TCP/IPv4)

### Steps Performed

| Step | Command/Tool | Finding |
|------|-------------|---------|
| 1 | ipconfig /all | DNS: 103.199.160.80 (ISP DNS) |
| 2 | nslookup google.com | DNS resolving correctly |
| 3 | nslookup youtube/facebook/8.8.8.8 | All resolved + reverse lookup confirmed |
| 4 | Set fake DNS (100.100.100.1) | DNS failure simulated — request timed out |
| 5 | Set Google DNS (8.8.8.8) | DNS restored — google.com resolved |
| 6 | ipconfig /flushdns | DNS cache cleared successfully |
| 7 | ipconfig /displaydns | Cache verified empty after flush |

### Key Findings
- Fake DNS IP causes complete resolution failure
- ISP DNS and Google DNS return different IPs for same domain
  — this is normal (load balancing)
- DNS failure looks like internet failure to end users
- /flushdns fixes stale cache issues after DNS changes

### Lessons Learned
- Always run nslookup first when user says internet is not working
- DNS failure ≠ internet failure — ping 8.8.8.8 to confirm connectivity
- Google DNS (8.8.8.8 / 8.8.4.4) is the standard manual fix
- ipconfig /flushdns resolves cached record issues instantly
