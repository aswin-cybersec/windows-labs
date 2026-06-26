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
