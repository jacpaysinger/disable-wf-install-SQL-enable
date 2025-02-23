# Disabling Windows Firewall and Installing SQL Server to Create Vulnerabilities

## Overview
This project explores security risks associated with misconfigured Windows environments by disabling Windows Firewall and installing SQL Server with insecure settings. The goal is to analyze logging, network accessibility, and potential attack vectors.

## Objectives  
- Disable Windows Firewall to expose the system to potential threats.  
- Install SQL Server with default, insecure credentials.  
- Enable logging for SQL Server and validate event collection.  
- Test network accessibility for Windows and Linux VM.
  
## Prerequisites
- An Azure account with a deployed VMs (Windows and Linux) with open Network Security Groups
- Admin access to `windows-vm`

  ## Environment Setup  

### 1. Remote Into the Windows VM 
I start by remoting into the Windows VM using RDP.  
<img width="471" alt="HP-11" src="https://github.com/user-attachments/assets/b56c0813-ad49-464a-9ecc-fe90c2a10c15" /><img width="559" alt="HP-12" src="https://github.com/user-attachments/assets/c9f9f764-861e-4802-b898-db97309f09ce" />

### 2. Disable Windows Firewall  
To introduce vulnerabilities, I disable the Windows Firewall under Domain, Private, and Public Profile
<img width="1048" alt="HP-17" src="https://github.com/user-attachments/assets/be4be5c5-6b0c-4e1e-a648-37043e2b7609" />


### 3. Install SQL Server (Evaluation Edition)
I install [SQL Server 2019 Evaluation](https://www.microsoft.com/en-us/evalcenter/evaluate-sql-server-2019) from Microsoft's Eval Center and use the following credentials:
  - **Username:** `*default*`
  - **Password:** `*Redacted*`
</br><img width="799" alt="HP-24" src="https://github.com/user-attachments/assets/7f67e56a-2914-42be-8044-589e01bd2e5a" />


### 4. Install SQL Server Management Studio (SSMS)
I install [SSMS](https://learn.microsoft.com/en-us/sql/ssms/download-sql-server-management-studio-ssms) from Microsoft's official site to manage and query the SQL database.


### 5. Enable SQL Server Logging
To track SQL Server activity in Windows Event Viewer, I enable logging:
- Open SQL Server Management Studio
- Connect to the database engine
- Navigate to `Security` → `Logins` → Right-click `sa`
- Enable **Failed Logins** tracking
- Ensure logs appear in Windows Event Viewer under `Applications and Services Logs -> MSSQLSERVER`


### 6. Test Connectivity to Linux VM
#### Ping the Linux VM:
To check network reachability, I attempt a ping from windows-vm:
```powershell
ping 20.62.45.75
```
<img width="866" alt="Screenshot 2025-02-22 at 9 54 11 PM" src="https://github.com/user-attachments/assets/2c341eaf-4f04-47fd-9fdc-5557ce1dd021" />


#### SSH into the Linux VM:
I then verify SSH access:
```bash

ssh labuser@20.62.45.75
```
<img width="800" alt="Screenshot 2025-02-22 at 9 58 57 PM" src="https://github.com/user-attachments/assets/eed80c65-957d-4aab-bad6-67b67c40b575" />

## Next Steps
These vulnerabilities set the stage for further exploitation and analysis in future projects. For now, I power off the VMs to conserve costs.

## Takeaways

- A disabled firewall exposes the system to unrestricted inbound threats.
- SQL Server default configurations can lead to credential-based attacks.
- Logging provides insight into unauthorized access attempts.
