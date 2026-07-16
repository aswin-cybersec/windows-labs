# Lab 02 — Windows System Diagnostics

## Objective
Perform Windows system diagnostics using built-in tools
to simulate real IT Support troubleshooting tasks.

## Environment
- VM: Windows 10 (VirtualBox)
- Network: VirtualBox NAT Network

## Tools Used
- Command Prompt (Admin)
- Event Viewer
- Services.msc
- Task Manager
- System File Checker (SFC)

## Steps Performed
| Step | Command/Tool | Finding |
|------|-------------|---------|
| 1 | ipconfig /all | DHCP enabled, DNS: ISP servers |
| 2 | systeminfo | Windows 10 Home, 2GB RAM, 5 hotfixes |
| 3 | Event Viewer | Event ID 7000 - WdiServiceHost failed |
| 4 | Services.msc | Restarted Windows Update service |
| 5 | Task Manager | High CPU — Windows Update background |
| 6 | sfc /scannow | Found and repaired corrupt system files |

## Key Findings
- Event ID 7000 = Service failed to start
- High CPU at idle caused by Windows Update
- sfc /scannow found and repaired corrupt files
- Normal behavior on new VM install

## Lessons Learned
- Always check Task Manager before assuming hardware failure
- sfc /scannow is the first response to system instability
- High CPU does not always mean malware
- Event Viewer is the primary log source for Windows diagnostics
