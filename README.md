# Fortigate 50 E-Internet-Configuration
Network Details
WAN IP: 10.12.34.211
WAN Gateway: 10.12.34.1
LAN IP: 192.168.1.99

Step 1: Connect to FortiGate
Plug your PC into Port1 (default LAN port).
Set your PC IP manually to 192.168.1.2, subnet 255.255.255.0.
Open a browser and go to https://192.168.1.99 
Username: admin
Password: leave Blank

Step 2
Set WAN Interface
Still in Network > Interfaces
Edit wan2 or the port connected to your ISP
Alias:INET-WAN2
Role: WAN
Addressing mode: Manual
IP/Netmask: 10.12.34.211/255.255.255.0

Administrative Access: Enable PING (Optional: HTTPS/SSH for remote admin)
Click OK

Step 3: Configure DNS
Go to Network > DNS
Primary DNS: 8.8.8.8
Secondary DNS: 4.2.2.2
Click Apply

Step 4: Set LAN Interface
Go to Network > Interfaces
Edit internal or lan interface (usually named internal or lan)
Alias:LAN
Role: LAN
IP/Netmask: 192.168.1.99/255.255.255.0
Administrative Access: Enable HTTPS, PING, SSH, and HTTP
Click OK

Step 5
Set Static Routes
Go to Network > Static Routes
Click Create New
Set:
Destination: 0.0.0.0/0 (This means default route)
Gateway: 10.12.34.1
Interface: wan2
Click OK

Step 6: Configure Firewall Policy (LAN → WAN)
Go to Policy & Objects > IPv4 Policy
Click Create New
Set:
Name: Policy1
Incoming Interface: LAN(lan)
Outgoing Interface: INET-WAN2(wan2)
Source: all
Destination: all
Schedule: always
Service: ALL
Action: Accept
Enable: NAT
Click OK

Step 7: Test the Internet
Connect a PC to the LAN
Set PC IP in range, e.g.:
IP: 192.168.1.100
Gateway: 192.168.1.99
Try to ping 8.8.8.8 or open a website

