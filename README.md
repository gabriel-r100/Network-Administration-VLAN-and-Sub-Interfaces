# Network-Administration-VLAN-and-Sub-Interfaces
![2024-02-08-Network-Diagram](https://github.com/gabriel-r100/Network-Administration-VLAN-and-Sub-Interfaces/assets/55646808/2aa94b86-77a5-4096-a22d-e81fa9914729)
<h1>Introduction</h1>
In this lab created in Cisco Packet Tracer, we are working on switch and router configurations that will segment the three departments and management plane.<br>
We are provided a subnet by our ISP of 64.35.35.0/29, with the ISP router IP address of 64.35.35.1 with a data VLAN of 222.

We were tasked with the following:
1. Create a VLAN for management of network equipment, these devices will not access the internet.
2. Configure each switch with an IP address to allow for remote access.
3. Each department should have their own subnet. (Provided on diagram)
4. Support computers will have static IPs set, while NOC and NE (Network Engineers) will have DHCP assigned IPs
5. Provide internet service to the computers on our network. (We emulate this by setting up a server with an 8.8.8.8 IP behind the ISP router)




<details>
    <summary><h2>Internet-Facing Interface and Creating a Default Route</h2></summary>
    1. We ensure the upstream physical port (g0/0) is up.<br>
    2. We then create a sub-interface of g0/0.222, with an dot1q encapsulation of VLAN 222 (as advised by the ISP), and set a static IP of 64.35.35.2 (second available IP from the given subnet).<br>
    3. Next we set a default route pointing to the ISP router at 64.35.35.1.<br>
    4. Finally, we test by pinging a Google DNS server at 8.8.8.8, this ensures that our gateway has an internet connection.<br>
    
   ![Upstream_Interface_Configuration](https://github.com/gabriel-r100/Network-Administration-VLAN-and-Sub-Interfaces/assets/55646808/01dde3a3-1b71-4503-ba8f-9b32bd408134)
</details>

![NetworkAdminLab-RouterPingingGoogleDNS](https://github.com/gabriel-r100/Network-Administration-VLAN-and-Sub-Interfaces/assets/55646808/d1f441dd-0e47-4351-9b85-c4b4a4543ec3)




<details>
    <summary><h2>Management IP, Segmented VLANs, Router Sub-Interfaces, and Testing Connectivity</h2></summary>
    
1. First I enable the internal port that will be the default gateway for our devices, create a sub-interface with VLAN 1000 for management of our network equipment and assign it the IP address of `10.251.251.1`.
   ![serverRouterVlan1000](https://github.com/gabriel-r100/Network-Administration-VLAN-and-Sub-Interfaces/assets/55646808/05b6fcb0-dde2-4c3f-9e75-0b045f44044e)
       
2. I then configure the server room switch uplink to be a trunk port, then I create an interface `VLAN1000`, create VLAN1000 on the switch, and assign interface `VLAN1000` an IP address of `10.251.251.2`. I also added the default router of `10.251.251.1` and confirm it can reach it by pinging the IP address.
   ![2-ConfigManagement-ServerRmSwitch](https://github.com/gabriel-r100/Network-Administration-VLAN-and-Sub-Interfaces/assets/55646808/6ea492c5-3f49-4e9f-af4a-833ec3fea69b)
    
3. Next, I configure the uplink port from the 1st floor switch to the server room switch. I create `VLAN 1000`, create the interface `VLAN1000`, assign it the IP address of `10.251.251.3`, add the default-gateway of 10.251.251.1, and test connectivity to our router. I repeat the same steps following the IP addresses on the network diagram.
   ![2-ConfigManagement-1stFloorSwitch-1](https://github.com/gabriel-r100/Network-Administration-VLAN-and-Sub-Interfaces/assets/55646808/17287d90-8834-4ca6-a0e2-64b3d3ec42cf)
    
4. After deciding which VLANs we will be using for each department, we add them to each of the switches, and create the sub-interfaces on the router for each VLAN.<br>
          a. VLAN1000 for management<br>
          b. VLAN50 for the support department<br>
          c. VLAN40 for the NOC department<br>
          d. VLAN30 for the NE department<br>
   ![2-ConfigManagement-ServerSW-VLAN-names](https://github.com/gabriel-r100/Network-Administration-VLAN-and-Sub-Interfaces/assets/55646808/fd664c9f-6700-44b7-843b-6c41141ba614)
   ![2-ConfigManagement-ServerRmRouter-Sub-Interfaces-1](https://github.com/gabriel-r100/Network-Administration-VLAN-and-Sub-Interfaces/assets/55646808/c70629bd-184d-4fd6-a7a2-5974d532738c)
    
5. I then add the VLANs to the 1st-3rd floor switches. For interfaces I know are going to house an endpoint, I set them to access mode and assign the proper VLAN.
        ![2-ConfigManagement-1stFloorSwitch-VLANs-AccessMode](https://github.com/gabriel-r100/Network-Administration-VLAN-and-Sub-Interfaces/assets/55646808/d120a3ee-b213-47cd-9fc1-baf8697f1e2c)
       
6. Finally, we statically assign IPs to the support department PCs and ensure they can reach the gateway on their vlan at `192.168.50.1`
   ![2-ConfigManagement-1stFloorSupportPC-ipconfig](https://github.com/gabriel-r100/Network-Administration-VLAN-and-Sub-Interfaces/assets/55646808/c77cf8d1-25ed-4138-80d6-4bc31a309f0b)
</details>

![NetworkAdminLab-InternalConnectivityTest](https://github.com/gabriel-r100/Network-Administration-VLAN-and-Sub-Interfaces/assets/55646808/5c550596-1add-443b-8bc2-37e4aaca756b)




<details>
<summary><h2>DHCP Reservations and Pools</h2></summary>
    
1. Creating DHCP reservation pools for our NOC (`192.168.40.0/24`) and NE (`192.168.30.0/24`) subnets. We reserve the first 10 IP address in the pools for static IP future uses.<br>
   ![3-NOC_DHCP_Pool](https://github.com/gabriel-r100/Network-Administration-VLAN-and-Sub-Interfaces/assets/55646808/48a15d7c-fefd-417a-896a-edf5690b9c6c)

2. I then confirm the switchport on the edgeswitch is set to access and the specific VLAN needed. (In this case, the NOC computer will be on VLAN 40)<br>
   ![1stFloorNOC-accessport](https://github.com/gabriel-r100/Network-Administration-VLAN-and-Sub-Interfaces/assets/55646808/088cd1ca-3437-4fb9-acf7-95821cd97197)

3. Lastly, I renew the IP address on the endpoints to receive a DHCP configuration.<br>
   ![1stFloorNOC-IPRenew](https://github.com/gabriel-r100/Network-Administration-VLAN-and-Sub-Interfaces/assets/55646808/9cfa9d4a-e47d-4745-8567-495dfca96104)

4. I repeat this step for the second DHCP pool and add the configuration to the remaining switches. Now all of our endpoints have an IP address.
</details>

![NetworkAdminLab-DHCP](https://github.com/gabriel-r100/Network-Administration-VLAN-and-Sub-Interfaces/assets/55646808/cfb818bf-7a9f-4df3-a07b-8f4a795891a9)





<details>
<summary><h2>Setting Up NAT Rules for Endpoint Internet Connectivity</h2></summary>
Now that all of our internal devices have IPs, we will create NAT rules to allow access to the internet for the computers.

1. Using the public IP pool we were provided (`64.35.35.0/29`), we create a NAT pool with the remaining public IPs we have.

   ![4-NATOutRule](https://github.com/gabriel-r100/Network-Administration-VLAN-and-Sub-Interfaces/assets/55646808/32bcc424-0d81-47a5-9109-278d575a1265)

2. Define the scope of IPs that will be allowed to leave our LAN (local area network) by creating an access list which includes only our endpoints' IP addresses.

   ![4-AccessList](https://github.com/gabriel-r100/Network-Administration-VLAN-and-Sub-Interfaces/assets/55646808/c7a471ba-6d0c-468e-b7d6-54c5f7b74fce)

3. I then create the NAT rule which allows devices without the access list to nat out using the public IP addresses, I also enable `overload` which will use PAT (port address translation) when the number of devices surpass the number of public IPs available. In most scenarios we will want to have this enabled as public IP address have a cost.

   ![4-NATRule](https://github.com/gabriel-r100/Network-Administration-VLAN-and-Sub-Interfaces/assets/55646808/ce77f2d2-0c26-4d56-97f1-843adf512f7d)

4. I then apply the `nat in` to the inward interfaces and `nat out` to the outside facing interface.

   ![4-NATInAndOut](https://github.com/gabriel-r100/Network-Administration-VLAN-and-Sub-Interfaces/assets/55646808/665dddaf-c52b-458a-b433-b7097c8abe93)

5. Lastly, I test connectivity to the internet. (Simulated here by pinging a GoogleDNS server IP that is outside of our network.)

   ![4-EndpointConnectivity](https://github.com/gabriel-r100/Network-Administration-VLAN-and-Sub-Interfaces/assets/55646808/ff3b5266-527f-478c-8e14-fb3ce247d137)

6. I also try pinging `8.8.8.8` from our switches to ensure that they are not able to communicate directly over the internet. They are not on our access list, therefore will not be able to NAT out of the LAN.

   ![4-1stFlrSwitchPingGoogle](https://github.com/gabriel-r100/Network-Administration-VLAN-and-Sub-Interfaces/assets/55646808/1ae3f9c7-8da6-4355-916a-5afc9494872e)

</details>




![NetworkAdminLab-FullyConfigured](https://github.com/gabriel-r100/Network-Administration-VLAN-and-Sub-Interfaces/assets/55646808/e632c31d-564b-409a-a629-c707ab228483)
