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

<img width="761" height="511" alt="2 enable-remote-desktop" src="https://github.com/user-attachments/assets/099a1b09-89d6-4943-a776-a13bec18d61d" />



## 3. Firewall Confirmation Rule

In the host VM go to powershell

-Open Powershell as admin
-```powershell
Enable-NetFirewallRule -DisplayGroup "Remote Desktop"

<img width="706" height="25" alt="image" src="https://github.com/user-attachments/assets/641b9b62-ca4f-4f86-9fb0-c7c0f8133312" />


## What the command does

- `Enable-NetFirewallRule` — Enables a Windows Firewall rule.
- `-DisplayGroup` — Specifies which group of firewall rules to modify.
- `"Remote Desktop"` — Selects the Remote Desktop firewall rules.

**Purpose:** Allows Remote Desktop traffic through the firewall so the client can connect to the host.

## 4. Test the Connection to the host

Go to powershell in the host PC

```powershell
Test-Connection 192.168.x.x -Port 3389
```

<img width="610" height="178" alt="4  test-connection" src="https://github.com/user-attachments/assets/e4457b95-cc27-4364-8d42-ba3b0ac903f0" />


### What the command does

- `Test-NetConnection` - Tests the network connectivity
- `192.168.x.x` - the host pc's ip address
- `Port 3389` - 3389 is the standard port for Remmote Desktop Protocol

Can the computer reach this Virtual Machine on RDP port 3389?

✅ TcpTestSucceeded : True = Your computer can reach port 3389 on the VM.


## 5. Connect with Remote Desktop via the Client's PC

- 'run' command in start menu
- Type `mstsc`
- Enter the host VM's ip address
- Enter credential of the host VM

<img width="405" height="238" alt="5 rd-sign-in" src="https://github.com/user-attachments/assets/609fa35f-b83b-4bf1-82c8-da1f3c540de6" />

<img width="451" height="397" alt="5 mstsc-rd " src="https://github.com/user-attachments/assets/d0d26160-d3cf-4a80-977d-1cb2d6a779e8" />


## 6. Create the new folder

In the Remote Desktop Protocol session:
- Open file explorer
- Go to `C:\CompanyData
- Right-click and choose **New > Folder**
- Name it "Remote Desktop Test Lab Folder"

<img width="939" height="585" alt="7 Remote-Desktop-folder creation" src="https://github.com/user-attachments/assets/7fbb91cb-d7a9-443b-9718-72c310ac7064" />

## 7. Sign out of RDP and Verify in Host VM

- Exit out of RDP from client's PC
- Connect to the host VM
- Verify if the new folder is there

  <img width="1022" height="380" alt="7  Verify-RDP-Folder-In-VM-Host" src="https://github.com/user-attachments/assets/3793daf6-a108-40c9-bdab-9f5985264e68" />

## What I learned

- RDP depends entirely if the network can be reached first before doing anything else.
- Enabling RDP through the GUI opens firewall automatically
- `Test-NetConnection` on port 3389 is quick way to see the problem with RDP
- Closing RDP window leaves the session running but signing out will end it

