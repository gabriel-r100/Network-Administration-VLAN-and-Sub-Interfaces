# Network-Administration-VLAN-and-Sub-Interfaces
![2024-02-08-Network-Diagram](https://github.com/gabriel-r100/Network-Administration-VLAN-and-Sub-Interfaces/assets/55646808/2aa94b86-77a5-4096-a22d-e81fa9914729)
## Introduction
In this lab created in Cisco Packet Tracer, we are working on switch and router configurations that will segment the three departments and management plane.
We are provided a subnet by our ISP of 64.35.35.0/29, with the ISP router IP address of 64.35.35.1. We were also advised that the data VLAN will be VLAN222.

We were tasked with the following:
1. Each department should have their own subnet.
2. Create VLAN1000 specifically for management of the network equipment.
3. Configure each switch with an IP address to allow for remote access.
4. Provide internet service throughout the network. (We emulate this by setting up a server with a 8.8.8.8 IP behind the ISP router)
5. Support computers will have static IPs set, while NOC and NE (Network Engineers) will have DHCP assigned IPs

