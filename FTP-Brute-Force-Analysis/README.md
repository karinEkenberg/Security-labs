# FTP Brute-Force Analysis

<img width="842" height="630" alt="hydra" src="https://github.com/user-attachments/assets/42c0b615-d818-4a8e-95ba-07e29920a566" />


````markdown

## Project Overview
This project demonstrates a dictionary attack against a vulnerable FTP service to highlight the risks of weak credentials.
The exercise was performed in a controlled lab environment using Kali Linux and Metasploitable 2.

## Technologies Used
* OS: Kali Linux
* Target: Metasploitable 2 (Virtual Machine)
* Tool: Hydra (Network logon cracker)
* Protocol: FTP (Port 21)

## Methodology
1.  Reconnaissance: Identified the target IP and open FTP port.
2.  Wordlist Creation: Created a targeted wordlist (`pass.txt`) containing common weak passwords.
3.  Execution: Launched Hydra to iterate through the wordlist against the `msfadmin` user.

## Command Executed
```bash
hydra -l msfadmin -P pass.txt ftp://192.168.160.128
````

## Result

Hydra successfully cracked the password (`msfadmin`) in under 4 seconds, confirming the vulnerability of the service configuration.

## Disclaimer

This project is for educational purposes and security research only.


