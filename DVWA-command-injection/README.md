# DVWA Command Injection (Remote Code Execution)

Project Overview

This project demonstrates a Command Injection vulnerability in the Damn Vulnerable Web App (DVWA). The objective was to exploit a poorly sanitized input field to execute arbitrary operating system commands on the hosting server.

Environment

    Attacker: Kali Linux (Firefox)

    Target: Metasploitable 2 (DVWA v1.0.7)

    Security Level: Low

Vulnerability Analysis

The application accepts user input (an IP address) and passes it directly to a system shell command (ping) without proper validation.

Vulnerable Logic: The backend likely executes: shell_exec( 'ping -c 4 ' . $user_input );

## Execution & Results

The testing process followed a three-step approach: establishing baseline functionality, injecting a command to identify the user, and finally escalating to arbitrary file reading.

1. Baseline Functionality Test

First, legitimate input was provided to confirm the application's intended behavior.

    Input: 127.0.0.1

    Result: The application performed a standard ping command, confirming the service was active.

<img width="673" height="401" alt="command-execution" src="https://github.com/user-attachments/assets/b7b9d5bd-b30e-41ff-90c4-0197abb6e2e5" />


2. Privilege Verification (whoami)

A command separator (;) was used to inject the whoami command to identify the executing user.

    Payload: 127.0.0.1; whoami

    Result: The output www-data confirmed code execution running under the web server's service account.

<img width="677" height="421" alt="command-execution-whoami" src="https://github.com/user-attachments/assets/83d3ea0d-b1e8-4b86-953f-cb244d699826" />


3. Information Disclosure (cat /etc/passwd)

To demonstrate the severity of the vulnerability, the system's user configuration file was accessed.

    Payload: 127.0.0.1; cat /etc/passwd

    Result: The server returned the contents of /etc/passwd, proving the ability to read sensitive files outside the web root.

<img width="536" height="677" alt="command-execution-read-files" src="https://github.com/user-attachments/assets/a1cf20a0-cd9a-48cc-8490-bea1cad5f778" />



Mitigation

To prevent Command Injection:

    Input Validation: Strictly validate that input matches expected formats (e.g., IPv4 regex).

    Avoid System Calls: Use built-in language functions instead of shell commands.

    Escaping: Use functions like escapeshellarg() to neutralize shell metacharacters before execution.
