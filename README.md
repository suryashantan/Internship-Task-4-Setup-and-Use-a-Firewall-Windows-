# Internship-Task-4-Setup-and-Use-a-Firewall-Windows-
This task involved configuring the Windows Defender Firewall to control network traffic. A specific rule was created to block inbound Telnet (TCP 23) traffic, which was then successfully tested using PowerShell (Test-NetConnection). 
Objective: Configure and test basic firewall rules (block and allow) to control network traffic.


Tool Used: Windows Defender Firewall with Advanced Security (GUI) and Windows PowerShell (for testing).

1. Firewall Configuration: Blocking Inbound Traffic (Port 23)
The goal of this step was to create an inbound rule to block the default Telnet port (TCP 23) to demonstrate a basic security control.

GUI Steps Used
Open Wizard: Opened "Windows Defender Firewall with Advanced Security" and selected Inbound Rules → New Rule...

Rule Type (task4 pic 2.png): Selected the Port option.

Protocol and Ports (task 4 pic3.png): Selected TCP and specified 23 for the "Specific local ports."

Action (task4 pic4.png): Selected Block the connection.

Name (PIC5.png): Named the rule "BLOCK TELNET 23 TEST" and clicked Finish.

Deliverable: Rule Applied
(You would include a screenshot here showing the final rule entry in the Inbound Rules list, similar to task 4 pic 1.png but showing the new rule.)

2. Testing the Block Rule
The connection test was performed locally using the loopback address (127.0.0.1), which directs the traffic back to the machine's own network stack, where the firewall intercepts it.

PowerShell Command and Result
Action	Command Used in PowerShell	Result
Test Block	Test-NetConnection -ComputerName 127.0.0.1 -Port 23	TcpTestSucceeded : False

Export to Sheets
Conclusion: The firewall successfully blocked the connection attempt to Port 23, confirming the rule is active and functioning correctly.

Deliverable: Test Screenshot
PIC 6.png clearly shows the command run and the desired output:

3. Adding an Allow Rule (SSH Port 22)
To demonstrate the opposite action, a rule was created to explicitly allow inbound traffic on the secure shell (SSH) port (TCP 22).

GUI Steps Used
Open Wizard: Opened the New Inbound Rule Wizard.

Rule Type: Selected Port.

Protocol and Ports: Selected TCP and specified 22 for the "Specific local ports."

Action: Selected Allow the connection.

Name: Named the rule "ALLOW SSH 22 TEST" and clicked Finish.

4. Cleanup and Restoration
The temporary firewall rules were removed to restore the system to its original state.

Action: Deleted the "BLOCK TELNET 23 TEST" and "ALLOW SSH 22 TEST" rules from the Inbound Rules list.

5. Summary: How a Firewall Filters Traffic
A firewall acts as a digital gatekeeper between a computer/network and external traffic, applying a set of rules to decide whether to allow or block data packets.

Inspection: Every incoming and outgoing data packet is inspected to check key information, including:

Source Address: Where the traffic came from (e.g., an external IP).

Destination Address/Port: Where the traffic is trying to go (e.g., your computer on Port 23).

Protocol: Whether it's TCP, UDP, ICMP, etc.

Rule Matching: The firewall compares the packet's attributes against its Access Control List (ACL), which is the prioritized list of rules you created.

Action:

If a packet matches a rule like "BLOCK TELNET 23 TEST", it is immediately dropped (denied access).

If a packet matches a rule like "ALLOW SSH 22 TEST", it is permitted to pass through.

Default Policy: If the packet doesn't match any explicit rule, the firewall applies its default policy. In Windows/Linux, the default policy for inbound connections is usually DENY for maximum security.

This filtering mechanism ensures that only authorized and necessary traffic reaches the protected system, preventing unauthorized connections and potential attacks.
