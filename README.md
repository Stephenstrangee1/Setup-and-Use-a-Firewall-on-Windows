# Cyber Security Internship Task 4: Setup and Use a Firewall on Windows/Linux

## Introduction
This repository documents my completion of Task 4 from the Elevate Labs Cyber Security Internship program. The objective was to configure and test basic firewall rules to allow or block traffic, using Windows Firewall on Windows 11. This exercise provided practical experience in network traffic filtering, port management, and security rule application.

Key learnings: Firewalls filter traffic based on rules for ports, protocols, and directions (inbound/outbound). Blocking insecure ports like Telnet (23) prevents risks from plain-text protocols, while allowing secure ones like SSH (22) enables safe remote access. I used PowerShell for precise command-line control, as it's more scriptable than the GUI.

## Tools Used
- **Windows Firewall**: Native tool on Windows, configured via PowerShell.
- **Operating System**: Windows 11.
- **PowerShell**: Run as Administrator for rule management.
- No additional paid tools or installations required.

## Steps Followed
I followed the task's Hints/Mini Guide step-by-step:

1. **Open Firewall Configuration Tool**: Launched PowerShell as Administrator to access Windows Firewall commands.
   
2. **List Current Firewall Rules**: Used `Get-NetFirewallRule` to display existing rules.
   - Screenshot: verify-rules-screenshot.png (Showing output of `Get-NetFirewallRule | Select DisplayName, Enabled, Direction, Action` with various system and custom rules).

3. **Add a Rule to Block Inbound Traffic on a Specific Port (e.g., 23 for Telnet)**: Created a rule to block port 23, as Telnet is insecure (transmits data in plain text).
   - Screenshot: block-port-23-screenshot.png (PowerShell output for `New-NetFirewallRule` command).

4. **Test the Rule by Attempting to Connect**: Since Telnet isn't enabled by default on Windows 11, I verified the rule's effect through status checks (e.g., via `Get-NetFirewallRule`). In a production test, I'd use `telnet localhost 23` or a remote probe to confirm blocking—no connection would establish.

5. **Add Rule to Allow SSH (Port 22)**: Added an inbound allow rule for port 22, simulating Linux-like SSH setup (useful if enabling OpenSSH on Windows).
   - Screenshot: allow-ssh-screenshot.png (PowerShell output for `New-NetFirewallRule` command).

6. **Remove the Test Block Rule**: Deleted the Telnet block rule to restore the original state.
   - Screenshot: remove-rule-screenshot.png (PowerShell execution of `Remove-NetFirewallRule`).

7. **Document Commands or GUI Steps Used**: All via PowerShell (preferred over GUI for reproducibility). Full commands in firewall_commands windows.txt; execution results in firewall_result windows.txt.

8. **Summarize How Firewall Filters Traffic**: Windows Firewall evaluates packets against rules: matching criteria like port (e.g., 23), protocol (TCP), direction (inbound), and action (block/allow). It's stateful, remembering connection contexts to allow replies without explicit rules. This filters out malicious traffic while permitting legitimate ones.

## Firewall Configuration Files and Outputs
- **Commands Script**: firewall_commands windows.txt – Contains all PowerShell commands used.
- **Results Output**: firewall_result windows.txt – Detailed console output showing rule creations, verifications, and removals. Includes excerpts like:
  - Custom rules: "Block Telnet" (Inbound, Block) and "Allow SSH" (Inbound, Allow).
  - System rules for context (e.g., Media Center, Steam).

## Answers to Interview Questions
To demonstrate deeper understanding:

1. **What is a firewall?** A network security system that monitors and controls incoming/outgoing traffic based on security rules, acting as a barrier against threats.
2. **Difference between stateful and stateless firewall?** Stateful firewalls track active connections and context (e.g., allowing return traffic); stateless ones evaluate packets individually without memory.
3. **What are inbound and outbound rules?** Inbound rules filter traffic entering the system; outbound rules filter traffic leaving it.
4. **How does UFW simplify firewall management?** UFW provides a straightforward CLI for managing iptables on Linux, with simple commands like `ufw allow 22/tcp` instead of complex syntax.
5. **Why block port 23 (Telnet)?** Telnet uses unencrypted communication, exposing credentials and data to interception; SSH (port 22) is a secure alternative.
6. **What are common firewall mistakes?** Creating overly broad rules, forgetting to enable the firewall, misordering rules, or not testing after changes.
7. **How does a firewall improve network security?** By blocking unauthorized access, limiting exposure to vulnerabilities, and enforcing policies to mitigate attacks like port scanning.
8. **What is NAT in firewalls?** Network Address Translation maps private IP addresses to a public one, hiding internal network structure and conserving IPs.

## Conclusion
This task built my skills in firewall configuration and traffic filtering, showing how rules protect against common risks. I successfully blocked an insecure port, allowed a secure one, and cleaned up, all documented with commands and screenshots. Future steps: Test with actual network tools like netcat for connection verification.
