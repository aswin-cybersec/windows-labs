# Lab 01 — Network Fundamentals

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
- netsh advfirewall

## Network Configuration
| Machine    | IP Address  | Gateway   |
|------------|-------------|-----------|
| Windows 10 | 10.0.2.3    | 10.0.2.1  |
| Kali Linux | 10.0.2.15   | 10.0.2.1  |

## Troubleshooting Methodology
1. Loopback test — 127.0.0.1
2. LAN connectivity — ping between VMs
3. Gateway test — ping 10.0.2.1
4. Internet connectivity — ping 8.8.8.8

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
- Windows Firewall blocks ICMP by default
- Added inbound ICMPv4 rule using netsh advfirewall
- TTL values identify device type:
  64 = Linux, 128 = Windows, 255 = Network device
- NAT mode isolates VMs — NAT Network mode required
  for inter-VM communication

## Lessons Learned
- Ping failure does not always mean device is offline
- Firewall rules can silently drop ICMP packets
- The 4-step ping sequence is the standard first response
  to any connectivity complaint in IT Support
