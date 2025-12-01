# Network Traffic Analysis: Telnet vs. SSH

This project demonstrates the security risks of cleartext protocols by analyzing traffic between **Kali Linux** and **Metasploitable 2** using **Wireshark**.

## Tools Used
* **Kali Linux** (Attacker/Client)
* **Metasploitable 2** (Vulnerable Target)
* **Wireshark** (Packet Analysis)

## Findings

### 1. Telnet (Unencrypted)
Traffic sent via Telnet is transmitted in **cleartext**.
* **Observation:** I could reconstruct the entire TCP stream.
* **Risk:** The server banner, login prompts, and credentials are fully visible to anyone listening on the network.

<img width="806" height="597" alt="kali-telnet" src="https://github.com/user-attachments/assets/5ef29c5f-2c84-47ec-b2fc-d1306027ed35" />


### 2. SSH (Encrypted)
Traffic sent via SSH is **encrypted**.
* **Observation:** The TCP stream shows the initial handshake (protocol negotiation), followed immediately by unreadable data.
* **Conclusion:** Even if the traffic is intercepted, the payload remains secure.

<img width="804" height="601" alt="kali-ssh" src="https://github.com/user-attachments/assets/7609f45e-e576-4ed9-8130-7b215e50588a" />

