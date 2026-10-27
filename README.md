# Setting-Up-RDP-Creating-A-New-Folder

# Summary 

This lab is setting Remote Desktop on a Windows Server 2025 (GUI) virtual machine, connected to it from my host PC using a built in RDP client and create a sub folder in `C:\CompanyData` 

# Environment 

- Host OS: Windows 11
- Hypervisor: VMware
- Host OS: WIndows Server 2025
- Client OS: PC 1
- VM Network Mode: Host-only
- VM IP Address: 192.168.x.x
- Account Used: Local Administrator

# Steps

## 1. Get the Host VM's IP Address
- Open PowerShell and run
```powershell
ipconfig
```
<img width="869" height="565" alt="Screenshot 2026-10-27 155553" src="https://github.com/user-attachments/assets/f6480166-b301-45e3-b52b-d6642b3a3435" />

## 2. Enable RDP on the Host VM

- Open Server Manager
- Local Server
- Click  `Remote Desktop`
- System Properties
- Allow remote connections to this computer
- `Remote Desktop` should be enabled


 <img width="766" height="506" alt="2  enable-rd" src="https://github.com/user-attachments/assets/52d7fc32-82ee-4da1-a8d8-a425e114e4dd" />

## 3. Firewall Confirmation Rule

In the host VM go to powershell

-Open Powershell as admin
-```powershell
Enable-NetFirewallRule -DisplayGroup "Remote Desktop"

<img width="706" height="25" alt="image" src="https://github.com/user-attachments/assets/641b9b62-ca4f-4f86-9fb0-c7c0f8133312" />


## What the command does

- `Enable-NetFireWallRule` - Alows a Windows Firewall Rule
- `DisplayGroup` - Specifies the group
- `"RemoteDesktop"` - Chooses the Remote Desktop firewall rules

Allows Remote Desktop traffic through the firewall so we can have the client connect to the host!


## 4. Test the Connection to the host

Go to powershell in the host PC

```powershell
Test-Connection 192.168.x.x -Port 3389
```

### What the command does

- `Test-NetConnection` - Tests the network connectivity
- `192.168.x.x` - the host pc's ip address
- `Port 3389` - 3389 is the standard port for Remmote Desktop Protocol

Can the computer reach this Virtual Machine on RDP port 3389?

✅ True = Your computer can reach port 3389 on the VM.



