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
**Repeat the above steps for the second layer 2 switch.**

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

- Now to configure the router R!
```
#configure terminal
#interface fastethernet 0/0
#no shutdown
#exit
#interface fastethernet 0/0.5
#encapsulation dot1q 5
#ip address 19
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

- Now to configure the PCs
- Type the following commands mentioned next to the PC name for each.
```
PC1 - ip 192.168.5.5 192.168.5.1/24
PC2 - ip 192.168.10.10 192.168.10.1/24
PC3 - ip 192.168.5.10 192.168.5.1/24
PC4 - ip 192.168.5.15 192.168.5.1/24
PC5 - ip 192.168.10.10 192.168.10.1/24 
```

## Switching
