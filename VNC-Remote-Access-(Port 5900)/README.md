# VNC Remote Access (Port 5900)

## Project Overview
This project targets the Virtual Network Computing (VNC) service running on port 5900. The objective was to demonstrate the security risk of weak credentials on remote desktop services by establishing an unauthorized graphical session.

## Environment
* **Attacker:** Kali Linux
* **Victim:** Metasploitable 2
* **Tools Used:** Nmap, vncviewer

## Execution & Analysis

### 1. Reconnaissance
Port 5900 was identified as open, running a VNC protocol service.
* **Command:** `nmap -p 5900 <target-ip>`
* **Result:** Port 5900/tcp open (vnc).

### 2. Credential Analysis
The service was configured with a weak, default password ("password"). In a real-world scenario, tools like Hydra would be used to audit this strength, but the service lockout policy demonstrated the risk of Denial of Service during aggressive scanning.

### 3. Exploitation (Remote Access)
Using the identified credentials, a remote graphical session was successfully established, granting full visibility of the target desktop.

* **Command:** `vncviewer <target-ip>`
* **Input:** Password entered manually.

<img width="1027" height="796" alt="VNC-Remote-Access" src="https://github.com/user-attachments/assets/491ca849-5265-43bb-85c2-0bdd3e0c51c4" />


## Mitigation
To secure VNC services:
1. **Strong Authentication:** Enforce complex passwords and consider multi-factor authentication if available.
2. **Tunneling:** Never expose VNC directly to the network. Use SSH Tunnels (VNC over SSH) to encrypt the traffic.
3. **Rate Limiting:** The "Too many authentication failures" error encountered during testing shows that rate limiting is present, but blocking the IP at the firewall level after failed attempts is a more robust solution.

## Disclaimer
This project is intended for educational purposes only. All testing was conducted on an isolated lab environment.
