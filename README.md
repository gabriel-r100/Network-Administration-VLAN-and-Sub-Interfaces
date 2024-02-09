# Network-Administration-VLAN-and-Sub-Interfaces
![2024-02-08-Network-Diagram](https://github.com/gabriel-r100/Network-Administration-VLAN-and-Sub-Interfaces/assets/55646808/2aa94b86-77a5-4096-a22d-e81fa9914729)
## Introduction
In this lab created in Cisco Packet Tracer, we are working on switch and router configurations that will segment the three departments and management plane.<br>
We are provided a subnet by our ISP of 64.35.35.0/29, with the ISP router IP address of 64.35.35.1 with a data VLAN of 222.

We were tasked with the following:
1. Create a VLAN for management of network equipment, these devices will not access the internet.
2. Configure each switch with an IP address to allow for remote access.
3. Each department should have their own subnet. (Provided on diagram)
4. Support computers will have static IPs set, while NOC and NE (Network Engineers) will have DHCP assigned IPs
5. Provide internet service to the computers on our network. (We emulate this by setting up a server with an 8.8.8.8 IP behind the ISP router)

## Configuring Upstream Interface and Creating a Default Route
1. We ensure the upstream physical port (g0/0) is up.
2. We then create a sub-interface of g0/0.222, with an dot1q encapsulation of VLAN 222 (as advised by the ISP), and set a static IP of 64.35.35.2 (second available IP from the given subnet).
3. Next we set a default route pointing to the ISP router at 64.35.35.1.
4. Finally, we test by pinging a Google DNS server at 8.8.8.8, this ensures that our gateway has an internet connection.

![Upstream_Interface_Configuration](https://github.com/gabriel-r100/Network-Administration-VLAN-and-Sub-Interfaces/assets/55646808/01dde3a3-1b71-4503-ba8f-9b32bd408134)

## Configuring Management VLAN and Management Sub-Interface

## Assign Private IP Addresses to Our Networking Equipment

## Setting up DHCP Pools and Static IP Pools for Our End Users

## Setting Up NAT Rules to Allow Access to the Internet (8.8.8.8)
