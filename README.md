🛡️ Cybersecurity Lab Setup: Kali Linux on VirtualBox

📖 1. Project Overview
This README documents the step-by-step process of building a virtual cybersecurity lab. The primary goal was to create an isolated and safe environment using VirtualBox and Kali Linux. This lab will be used for future penetration testing, network reconnaissance, and vulnerability assessments without affecting the host machine.

🎯 2. Lab Objectives
Install VirtualBox as the hypervisor.

Set up a custom NAT Network to allow future VMs (like target machines) to communicate with each other.

Import and configure Kali Linux.

Assign a static IP address for consistent access.

Test and troubleshoot network connectivity.

Take a clean snapshot of the working machine.

⚙️ 3. Lab Configuration
Component                     	Details
Host System	                    Windows 11
Hypervisor	                    VirtualBox 7.2
Guest OS	                    Kali Linux 20262
VM RAM	                        2048 MB
Network Type                	NAT Network
Subnet	                        10.0.0.0/24
Kali IP Address	                10.0.0.2 (Static)
Gateway	                        10.0.0.1
DNS Server	                    8.8.8.8


🚀 4. Setup Process
Step 1: VirtualBox NAT Network Configuration
A dedicated NAT Network was created to ensure that multiple VMs can communicate with each other while still having internet access. This is essential for a multi-machine lab.


`![](2-screenshot network settings 1.png)`

Step 2: Kali Linux VM Settings
The Kali Linux VM was imported, and its network adapter was attached to the "NatNetwork".


`![](vm-network-adapter.png)`

Step 3: Static IP Configuration
Inside Kali Linux, the IPv4 settings were manually configured to use a static IP. This ensures the machine is always reachable at 10.0.0.2.

`![](4-screenshot kali network settings.png)`

Step 4: Taking a Baseline Snapshot
Once the network was working, a snapshot was created named "My fresh kali linux". The description states that the IP addresses are set and the internet is working fine. This serves as a recovery point.


`![](snapshot-creation.png)`

🔍 5. Verification & Troubleshooting
Network Connectivity Fix
After setting the static IP, I encountered a minor issue where the internet connection dropped. I used the nmcli command in the Kali terminal to modify the connection and restart it.

Commands executed:

bash
sudo nmcli connection modify "Wired connection 1" ipv4.dad-timeout 0
sudo nmcli connection down "Wired connection 1"
sudo nmcli connection up "Wired connection 1"

`![](kali-terminal-fix.png)`

Final Verification Tests
ping 10.0.0.1 (Gateway) - Successful

ping 8.8.8.8 (Internet) - Successful

nslookup networkwalks.com (DNS) - Successful

Kali Linux Desktop
The final working environment looks like this:


![](C:\Users\karan\OneDrive\Desktop\network walks\week 1\kali linux.png)
`![ Practical ] (kali-desktop.png)`
![](kali-desktop.png)

🐞 6. Other Issues Faced
VirtualBox VT-x Error: Initially, the VM failed to start because hardware virtualization was disabled in my BIOS. I fixed this by rebooting, entering the BIOS/UEFI, enabling Intel VT-x, and saving the settings.

💡 7. Key Learnings
Networking: Gained a clear understanding of how NAT Networks work and why they are better than standard NAT for lab environments.

Linux CLI: Learned how to troubleshoot network issues using nmcli.

Documentation: Realized the importance of taking screenshots and documenting errors and fixes.

📝 Project Information
Author: Vaja Karan

Program: Cybersecurity at Networkwalks

Week: 01

Project: Cybersecurity & Pentesting Lab Setup
