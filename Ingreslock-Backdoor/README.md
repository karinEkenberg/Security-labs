# Ingreslock Backdoor Analysis (Port 1524)

## Project Overview
This project documents the discovery and utilization of a misconfigured service on port 1524 (Ingreslock) on a Metasploitable 2 target. 
The service provided direct root access without authentication, demonstrating the danger of leaving debug ports open.

## Methodology

### 1. Reconnaissance
A targeted Nmap scan was performed on port 1524.

* **Command:** `nmap -p 1524 -sV <target-ip>`
* **Result:** The service was identified as a "Bindshell" giving direct access to the system.

### 2. Exploitation
Unlike typical exploitation requiring payloads, this vulnerability was exploited by simply connecting to the port using Netcat.

* **Tool:** Netcat (nc)
* **Command:** `nc <target-ip> 1524`

### 3. Verification
Upon connection, a command shell was immediately available.

* **Command:** `whoami` -> **root**
* **Command:** `hostname` -> **metasploitable**

<img width="662" height="537" alt="ingreslock-backdoor" src="https://github.com/user-attachments/assets/16c093d4-ba7b-41af-8c8b-eb1b730c8a64" />


## Mitigation
To secure the system:
1. Identify the process listening on port 1524.
2. Terminate the unauthorized process.
3. Configure firewall rules to block traffic on non-essential ports.

## Disclaimer
This project is intended for educational purposes only. All testing was conducted on an isolated lab environment.
