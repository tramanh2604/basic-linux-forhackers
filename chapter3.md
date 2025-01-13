# CHAP 3: ANALYZING & MANAGING NETWORKS

## 1. Analyzing networks with ifconfig

![ifconfig](../images/ifconfig.png)

1) eth0: short for EthernetO. This's the first wired network connection. If there were more wired Ethernet interfaces, they would show up in the output eth1, eth2...

The type of network being used (ethernet) is listed here, HWaddr and an adress - NIC/MAC

2) IP address

3) Broadcast address, used to send out information to all IPs on the subnet

4) network mask: which is used to determine what part of IP address is connected to the local network.

5) lo: short for localhost. This's a specical software address that connects you to your own system. 

6) wlan0: It only appears if you have a wireless interface or adapter. 

=> ifconfig enables you to connect to and manipulate your LAN settings

## 2. Checking wireless network devices with iwconfig
- You can use the iwconfig to gather crucial information for wireless hacking as the adapter's IP address, its MAC address, what mode it's in...

1) wlan0: that the only network interface with wireless exrensions. We learn that 802.11 IEEE wireless standards our device is capable of: b and g (n is the lastest standard).

Neither lo nor eth0 has any wireless extensions.

2) The mode of the wireless extension: managed.

3) The wireless adapter is not connected: Not Associated

4) Its power is 20 dBm - represents the strength of signal.

3. Changing your network information
1) Changing your IP address.

- To change your IP address, enter ifconfig followed by the interface you want to reassign and the new IP address you want to assigned to that interface.

Ex: to assign the IP address 192.168.181.115 to interface eth0, you would enter:
ifconfig eth0 192.168.181.115

Then you check again with ifconfig, you should see that your IP address has changed.

## 3. Changing your network information
