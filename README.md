# Cyber Security Internship Task 4: Setup and Use a Firewall on Windows

## Introduction
This repository documents my completion of Task 4 from the Elevate Labs Cyber Security Internship program. The objective was to configure and test basic firewall rules on Windows to allow or block network traffic, gaining hands-on experience with firewall management and traffic filtering.

Key learnings: Firewalls act as barriers to control incoming and outgoing traffic based on rules, helping prevent unauthorized access. I used Windows Firewall via PowerShell on Windows 11, focusing on blocking insecure ports like Telnet (23) and allowing secure ones like SSH (22), even though SSH is more common on Linux—this demonstrates rule creation flexibility.

## Tools Used
- **Windows Firewall**: Built-in firewall tool accessed via PowerShell (no additional installations needed).
- **Operating System**: Windows 11.
- **PowerShell**: Run as Administrator for configuring rules.
- No paid tools or external software required.

## Steps Followed
I followed the task's Hints/Mini Guide step-by-step, using PowerShell commands for Windows:

1. **Open Firewall Configuration Tool**: Launched PowerShell as Administrator.
   - Screenshot: [Firewall Configuration Overview] (Showing initial Get-NetFirewallRule output).

2. **List Current Firewall Rules**: Used `Get-NetFirewallRule` to view existing rules.
   - Commands: See [firewall_commands windows.txt](firewall_commands_windows.txt).
   - Results: See truncated output in [firewall_result_windows.txt](firewall_result_windows.txt), showing rules like "Cast to Device" and custom ones added later.

3. **Add a Rule to Block Inbound Traffic on a Specific Port (e.g., 23 for Telnet)**: Created a block rule for port 23 (Telnet, insecure due to plain-text transmission).
   - Command: `New-NetFirewallRule -DisplayName "Block Telnet" -Direction Inbound -LocalPort 23 -Protocol TCP -Action Block`
   - Screenshot: [Block Inbound on Port 23] (PowerShell output confirming rule creation).

4. **Test the Rule**: Attempted a local Telnet connection using `telnet localhost 23` (or remotely if setup), but since Telnet isn't enabled by default on Windows 11, verified via rule status. In a real test, it would block connections.
   - Note: For safety, tested in a controlled environment; no actual remote test shown as per local setup.

5. **Add Rule to Allow SSH (Port 22)**: Even on Windows, added an allow rule for port 22 (SSH, for potential OpenSSH server use).
   - Command: `New-NetFirewallRule -DisplayName "Allow SSH" -Direction Inbound -LocalPort 22 -Protocol TCP -Action Allow`
   - Screenshot: [Allow SSH on Port 22] (PowerShell output confirming rule creation).

6. **Remove the Test Block Rule**: Restored original state by removing the Telnet block rule.
   - Command: `Remove-NetFirewallRule -DisplayName "Block Telnet"`
   - Screenshot: [Remove Test Rule] (PowerShell execution).

7. **Document Commands or GUI Steps Used**: All steps via PowerShell (no GUI for precision). Full commands in [firewall_commands_windows.txt](firewall_commands_windows.txt); results in [firewall_result_windows.txt](firewall_result_windows.txt).

8. **Summarize How Firewall Filters Traffic**: Firewalls inspect packets based on rules (e.g., source/destination IP, port, protocol). Inbound rules control incoming traffic (e.g., block port 23 to prevent external Telnet exploits), while outbound rules manage outgoing (e.g., allow specific apps). Windows Firewall is stateful, tracking connections for dynamic responses.

## Firewall Rules Summary
- **Viewed Rules**: Used `Get-NetFirewallRule | Select DisplayName, Enabled, Direction, Action` to verify.
  - Example Output (from [firewall_result_windows.txt](firewall_result_windows.txt)):
    - Block Telnet: True, Inbound, Block
    - Allow SSH: True, Inbound, Allow
    - Other system rules (e.g., Steam, Google Chrome) shown for context.
- **Custom Rules Added/Removed**: Successfully created, verified, and cleaned up to avoid persistent changes.
- No issues encountered; rules parsed successfully (Status: OK).

## Answers to Interview Questions
To demonstrate deeper understanding:

1. **What is a firewall?** A security system that monitors and controls network traffic based on predetermined rules, acting as a barrier between trusted and untrusted networks.

2. **Difference between stateful and stateless firewall?** Stateless firewalls filter packets independently without context; stateful ones track connection states for more intelligent decisions (e.g., allowing responses to initiated traffic).

3. **What are inbound and outbound rules?** Inbound rules govern incoming traffic to the device; outbound rules control traffic leaving the device.

4. **How does UFW simplify firewall management?** UFW (Uncomplicated Firewall) provides a user-friendly interface to iptables on Linux, allowing simple commands like `ufw allow 22` instead of complex syntax.

5. **Why block port 23 (Telnet)?** Telnet transmits data in plain text, making it vulnerable to eavesdropping and man-in-the-middle attacks; better to use secure alternatives like SSH.

6. **What are common firewall mistakes?** Overly permissive rules (allowing all traffic), forgetting to test rules, ignoring outbound controls, or misconfiguring NAT/port forwarding.

7. **How does a firewall improve network security?** By blocking unauthorized access, preventing malware spread, and enforcing policies to filter malicious traffic.

8. **What is NAT in firewalls?** Network Address Translation rewrites IP addresses in packets, hiding internal networks behind a single public IP for added security and IP conservation.

## Conclusion
This task provided basic firewall management skills, emphasizing the role of rules in traffic filtering. I focused on Windows PowerShell for precise control, blocking insecure Telnet and allowing SSH as a best practice. Future improvements: Integrate with GUI for visual verification or test with actual connections.
