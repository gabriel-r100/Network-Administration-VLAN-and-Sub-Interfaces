# Network-Administration-VLAN-and-Sub-Interfaces
![2024-02-08-Network-Diagram](https://github.com/gabriel-r100/Network-Administration-VLAN-and-Sub-Interfaces/assets/55646808/2aa94b86-77a5-4096-a22d-e81fa9914729)
## Introduction
In this lab created in Cisco Packet Tracer, we are working on switch and router configurations that will segment the three departments and management plane.<br>
We are provided a subnet by our ISP of 64.35.35.0/29, with the ISP router IP address of 64.35.35.1 with a data VLAN of 222.

We were tasked with the following:
1. Each department should have their own subnet. (Provided on diagram)
2. Create VLAN1000 specifically for management of the network equipment.
3. Configure each switch with an IP address to allow for remote access.
4. Provide internet service throughout the network. (We emulate this by setting up a server with an 8.8.8.8 IP behind the ISP router)
5. Support computers will have static IPs set, while NOC and NE (Network Engineers) will have DHCP assigned IPs

## Configuring Upstream Interface and Creating a Default Route
1. We ensure the upstream physical port (g0/0) is up.
2. We then create a sub-interface of g0/0.222, with an dot1q encapsulation of VLAN 222 (as advised by the ISP), and set a static IP of 64.35.35.2 (second available IP from the given subnet).
3. Next we set a default route pointing to the ISP router at 64.35.35.1.
4. Finally, we test by pinging a Google DNS server at 8.8.8.8

![Upstream_Interface_Configuration](https://github.com/gabriel-r100/Network-Administration-VLAN-and-Sub-Interfaces/assets/55646808/01dde3a3-1b71-4503-ba8f-9b32bd408134)
