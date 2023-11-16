# CCN_Project_5th_Sem_VLAN GNS3


![image](https://github.com/AniruddhaN2203/CCN_Project_5th_Sem_VLAN/assets/142299140/b6725d4d-3ad5-49c3-8626-39aa8775e6ef)

## Configuring the VLAN Network

### Layer 2 Switches
- First draw the above network and turn on all the devices
- Double click on the first layer 2 switch and type the following
```
>enable
#configure terminal
#vlan 5
#name go
#exit

>enable
#configure terminal
#vlan 10
#name juu
#exit(two times)
#wr me
```
- Repeat the above steps for the second layer 2 switch.

- Next type the following commands to configure the linking for the first layer 2 switch
```
#configure terminal
#interface gigabitethernet 0/1
#switchport mode access
#switchport access vlan 5
#exit

#interface gigabitethernet 0/2
#switchport mode access
#switchport access vlan 10
#exit

#interface gigabitethernet 0/3
#switchport trunk encapsulation dot1q
#switchport mode trunk
#exit

#interface gigabitethernet 0/0
#switchport trunk encapsulation dot1q
#switchport mode trunk
#exit
#exit
#wr me
```

- The next few commands are for the second layer 2 switch
```
#configure terminal
#interface gigabitethernet 0/1
#switchport mode access
#switchport access vlan 5
#exit

#interface gigabitethernet 0/2
#switchport mode access
#switchport access vlan 5
#exit

#interface gigabitethernet 0/3
#switchport mode access
#switchport access vlan 10
#exit

#interface gigabitethernet 0/0
#switchport trunk encapsulation dot1q
#switchport mode trunk
#exit
#exit
#wr me
```

**Trunk and Access Mode Connections**
- Trunk connections are used to interconnect switches and routers and carry traffic for multiple VLANs. They allow the passage of VLAN-tagged frames between devices, helping to maintain VLAN segregation across the network.
- Access mode connections are used for devices that are members of a specific VLAN. Traffic entering and leaving an access mode port is assumed to be part of the VLAN configured on that port.

### Router
- Now to configure the router R1
```
#configure terminal
#interface fastethernet 0/0
#no shutdown
#exit
#interface fastethernet 0/0.5
#encapsulation dot1q 5
#ip address 192.168.5.1 255.255.255.0
#no shutdown
#exit
#interface fastethernet 0/0.10
#encapsulation dot1q 10
#ip address 192.168.10.1 255.255.255.0
#no shutdown
#end
#wr me
```

### PCs
- Now to configure the PCs
- Type the following commands mentioned next to the PC name for each.
```
PC1 - ip 192.168.5.5 192.168.5.1/24
PC2 - ip 192.168.10.10 192.168.10.1/24
PC3 - ip 192.168.5.10 192.168.5.1/24
PC4 - ip 192.168.5.15 192.168.5.1/24
PC5 - ip 192.168.10.15 192.168.10.1/24 
```

## Switching
### Intra VLAN Switching
- Intra VLAN switching refers to the process of forwarding network traffic between devices within the same VLAN. 
- Switches operate at Layer 2 (Data Link layer) of the OSI model and are responsible for making forwarding decisions based on MAC (Media Access Control) addresses.

![image](https://github.com/AniruddhaN2203/CCN_Project_5th_Sem_VLAN/assets/142299140/49b3d1e6-72ee-4e63-9833-fea34a004dea)
- We turn the router off here as we need to demonstrate switching in the same VLAN.

**Juu**
- We will take PC2 which is part of VLAN 10(name - juu).
- We ping PC5 which also part of the same VLAN and capture the packets on the trunk connection between the two switches.

![image](https://github.com/AniruddhaN2203/CCN_Project_5th_Sem_VLAN/assets/142299140/45fbc470-f6e7-405c-a8a5-f4ab54ff09f1)

![image](https://github.com/AniruddhaN2203/CCN_Project_5th_Sem_VLAN/assets/142299140/2cc41b98-6ccc-4e06-815c-3d9871d20cfa)
- As we can see the packets are captured on the link.

**Go**
- We will take PC1 which is part of VLAN 5(name - go).
- We ping PC4 which also part of the same VLAN and capture the packets on the trunk connection between the two switches.

![image](https://github.com/AniruddhaN2203/CCN_Project_5th_Sem_VLAN/assets/142299140/7b80c6e9-d1d0-4925-993f-ca214b84b062)

![image](https://github.com/AniruddhaN2203/CCN_Project_5th_Sem_VLAN/assets/142299140/7d49bc48-a9ca-4a23-8bfa-873540350ffb)
- As we can see the packets are captured on the link.

**Juu to Go**

![image](https://github.com/AniruddhaN2203/CCN_Project_5th_Sem_VLAN/assets/142299140/9b4cc19e-fa39-4827-8a4e-e49c255df7dc)
- If we try pinging PC2 or PC5 it won't work as inter VLAN switching operates on routers or Layer 3 (Network Layer) switches

### Inter VLAN Switching

![image](https://github.com/AniruddhaN2203/CCN_Project_5th_Sem_VLAN/assets/142299140/aa961b38-0439-4a4b-882e-b0e77c157870)
- Inter-VLAN switching refers to the process of forwarding network traffic between different VLANs.
- When communication needs to occur between devices in different VLANs, a layer 3 device, typically a router or layer 3 switch, is required to perform inter-VLAN routing.
- For traffic that requires routing between different VLANs, the router uses the destination IP address to make forwarding decisions. The switch looks at the destination IP address of the packet and determines the appropriate next-hop or outgoing interface based on its routing table.
- We capture the packets on the trunk connection connected to the router as that is what facilitates inter vlan switching

**Go to Juu**

![image](https://github.com/AniruddhaN2203/CCN_Project_5th_Sem_VLAN/assets/142299140/af943d34-4180-44c9-8a68-86bef5b12dc7)

![image](https://github.com/AniruddhaN2203/CCN_Project_5th_Sem_VLAN/assets/142299140/7cbe4c00-9b47-4b04-a4b3-50a77ef59d42)

- We are pinging PC5 from PC1.
- As we can see the packets are captured on the trunk connection present on the router

## Addressing
### MAC Addressing:

![image](https://github.com/AniruddhaN2203/CCN_Project_5th_Sem_VLAN/assets/142299140/7a93b0ff-ca2d-4aa6-9b2e-0c15a4301a97)
- ```show mac address-table``` is the command used to see the MAC addresses that the switch has learnt about
- In VLANs, MAC addressing is crucial for the operation of Layer 2 switches.
- Switches use MAC addresses to forward frames within the same VLAN. The MAC address table in a switch associates MAC addresses with the corresponding switch ports, allowing the switch to make forwarding decisions based on these addresses.

### IP Addressing:
- We can refer to the section of router configuration and PC configuration for this.
- VLANs are often associated with IP subnets. Devices within the same VLAN typically share the same IP subnet, and devices in different VLANs often belong to different IP subnets.
- IP addressing is essential for Layer 3 devices like routers that route traffic between different VLANs.
- Routers use IP addresses to make routing decisions and facilitate communication between devices in different VLANs. Each VLAN may be associated with a different IP subnet, allowing for logical network segmentation.

### VLAN Tagging
- Again for this section we can refer to the Switch and Router configuration
- We can analyze the following command ```encapsulation dot1q 10```.
- Encapsulation : Encapsulation is crucial for tagging frames with VLAN information so that switches can understand which VLAN a frame belongs to.
- dot1q : The dot1q in the command refers to IEEE 802.1Q, which is the industry standard for VLAN tagging. IEEE 802.1Q is a protocol that adds a 4-byte tag to Ethernet frames, providing VLAN identification information. The tag includes a VLAN ID, allowing switches to understand which VLAN a frame belongs to and, consequently, how to handle and forward the frame within the VLAN-aware network.
- 10 - This is the VLAN tag/ID that is associated with VLAN 10(name - juu).

## Filtering
- Filtering refers to the process of controlling and managing the flow of traffic between different VLANs.
- Filtering mechanisms are used to determine which types of traffic are allowed or denied between VLANs, providing a level of security and control over communication within a network.

**Using ACL(Access Control List)**

![image](https://github.com/AniruddhaN2203/CCN_Project_5th_Sem_VLAN/assets/142299140/a6e639e4-cae0-4d98-807d-fd5dbf5f6dc7)
- ```$ -> access-list```
- We need to type the following commands in the router.
- This will block access from VLAN 5(go) to VLAN 10(juu).

![image](https://github.com/AniruddhaN2203/CCN_Project_5th_Sem_VLAN/assets/142299140/aaa1163c-739e-447f-8623-d8dc683dc315)
- As we can see inter VLAN routing is not possible but intra VLAN routing is possible.

![image](https://github.com/AniruddhaN2203/CCN_Project_5th_Sem_VLAN/assets/142299140/aea5f9ca-03ad-4332-aa76-52dc6a3fa4ec)
- To give access back to the VLAN type the above commands.
- This will permit access from VLAN 5(go) to VLAN 10(juu).


## Acknowledgments
- Website - https://www.sysnettechsolutions.com/en/configure-vlan-in-layer-2-switch/
- Download Layer 2 Switch - https://www.sysnettechsolutions.com/en/download-vios-l2-image-for-gns3/
