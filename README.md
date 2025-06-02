<p align="center">
<img src="https://i.imgur.com/YOUR_WIRESHARK_LOGO.png" alt="Wireshark Logo"/>
</p>
<h1>Network Security Groups (NSGs) and Inspecting Traffic Between Azure Virtual Machines</h1>
This tutorial outlines the process of observing network traffic to and from Azure Virtual Machines using Wireshark and experimenting with Network Security Groups (NSGs) to control traffic. This project was completed as part of the CourseCareers IT course to demonstrate skills in network analysis, cloud security, and virtual machine configuration.

<h2>Environments and Technologies Used</h2>
Microsoft Azure (Virtual Machines/Compute)

Remote Desktop

Various Command-Line Tools (e.g., ping, nslookup, ssh)

Various Network Protocols (SSH, RDP, DNS, HTTP/S, ICMP)

Wireshark (Protocol Analyzer)

<h2>Operating Systems Used</h2>
Windows 11 (21H2)

Ubuntu Server 20.04

<h2>High-Level Steps</h2>
Provision Azure Virtual Machines: Set up a Windows 11 VM and an Ubuntu Server 20.04 VM in the same virtual network.

Install Wireshark: Install Wireshark on the Windows 11 VM to capture and analyze network traffic.

Generate and Observe Traffic: Use command-line tools to generate traffic (e.g., ICMP, DNS, HTTP/S) between VMs and analyze it with Wireshark.

Configure and Test NSGs: Create and modify NSG rules to control traffic flow and observe the impact on connectivity.

<h2>Actions and Observations</h2>

<p>
<b>Step 1: Provision Azure Virtual Machines</b><br />
- Log in to the Microsoft Azure portal and create two virtual machines:
  - **Win-VM**: Windows 11 (21H2) with at least 2 vCPUs and 4GB RAM.
  - **Ubuntu-VM**: Ubuntu Server 20.04 with at least 1 vCPU and 2GB RAM.
- Place both VMs in the same virtual network (VNet) and subnet to allow communication.
- Assign static private IP addresses to ensure consistent addressing (e.g., Win-VM: 10.0.0.4, Ubuntu-VM: 10.0.0.5).
- Enable Remote Desktop Protocol (RDP) for Win-VM and SSH for Ubuntu-VM.
- Connect to Win-VM via Remote Desktop and Ubuntu-VM via SSH to verify connectivity.
</p>
<br />

<p>
<b>Step 2: Install Wireshark</b><br />
- On the Win-VM, download and install Wireshark from the official website (https://www.wireshark.org).
- Select the network interface connected to the Azure VNet (e.g., Ethernet adapter) for packet capture.
- Start a capture session to verify that Wireshark can detect network traffic.
- Test basic connectivity by pinging the Ubuntu-VM (e.g., `ping 10.0.0.5`) and confirm ICMP packets appear in Wireshark.
</p>
<br />

<p>
<b>Step 3: Generate and Observe Network Traffic</b><br />
- From the Win-VM, use command-line tools to generate various types of network traffic:
  - **ICMP**: Run `ping 10.0.0.5` to send ICMP echo requests to the Ubuntu-VM.
  - **DNS**: Run `nslookup google.com` to generate DNS queries.
  - **HTTP/S**: Open a browser and navigate to a website (e.g., https://example.com) to capture HTTP/S traffic.
  - **RDP**: Connect to the Win-VM via RDP to observe RDP traffic.
  - **SSH**: Connect to the Ubuntu-VM via SSH (e.g., `ssh user@10.0.0.5`) to capture SSH traffic.
- In Wireshark, apply filters (e.g., `icmp`, `dns`, `http`, `tcp.port == 3389`, `tcp.port == 22`) to isolate and analyze each protocol.
- Observations:
  - ICMP packets show ping requests and replies between VMs.
  - DNS queries resolve domain names to IP addresses.
  - HTTP/S traffic includes TCP handshakes and encrypted data.
  - RDP and SSH traffic show encrypted session establishment.
</p>
<br />

<p>
<b>Step 4: Configure and Test Network Security Groups</b><br />
- In the Azure portal, create a Network Security Group (NSG) and associate it with the subnet containing both VMs.
- Add an inbound rule to allow specific traffic (e.g., allow ICMP, port 3389 for RDP, port 22 for SSH).
- Test connectivity (e.g., ping Ubuntu-VM, RDP to Win-VM, SSH to Ubuntu-VM) and verify traffic in Wireshark.
- Modify NSG rules to block specific traffic:
  - Add a rule to deny ICMP (priority 100, protocol ICMP, action Deny).
  - Test ping from Win-VM to Ubuntu-VM and observe failure in connectivity.
  - Confirm in Wireshark that ICMP packets are no longer received.
- Revert the rule to allow ICMP and verify restored connectivity.
- Observations:
  - NSG rules effectively control traffic flow based on protocol, port, and source/destination.
  - Blocking ICMP prevents ping responses, visible in Wireshark as unanswered requests.
</p>
<br />
<h2>Testing and Validation</h2>

<p>
<b>Step 5: Testing and Validation</b><br />
- Tested multiple network protocols (ICMP, DNS, HTTP/S, RDP, SSH) to ensure accurate capture and analysis in Wireshark.
- Validated NSG rule enforcement by toggling allow/deny rules for ICMP and observing connectivity changes.
- Confirmed RDP and SSH access to VMs before and after NSG rule changes.
- Used Wireshark filters to isolate specific traffic types and analyze packet details (e.g., source/destination IPs, ports, payload).
- Verified DNS resolution and HTTP/S traffic to external sites, ensuring proper network configuration.
</p>
<br />
<h2>Project Outcome</h2>
This project demonstrates proficiency in network analysis and cloud security using Microsoft Azure, Wireshark, and NSGs. Key skills include provisioning Azure VMs, capturing and analyzing network traffic with Wireshark, and configuring NSG rules to control traffic flow in a cloud environment.

