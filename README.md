# DHCP-Server-with-PFSense
![image](https://github.com/hasankilic0663/DHCP-Server-with-PFSense/assets/101570706/ef2ff67f-53a9-423e-a2d5-78afbe952a2f)
![thredas2](https://github.com/hasankilic0663/DHCP-Server-with-PFSense/assets/101570706/1f0fdb8d-1972-49fe-9867-6638f4489dcb)
adasdasdasdan
## Terminology

Before we begin the setup of our DHCP and FTP server, we need to understand some terms.

### Network

A network consists of two or more computers connected together to share resources (such as printers and CDs), exchange files, or allow electronic communication. Computers in a network can be connected via cables, telephone lines, radio waves, satellites, or infrared light beams.

### LAN and Subnet

LAN (Local Area Network) refers to a group of devices connected within a specific physical location or network segment. It usually represents a single network infrastructure that allows devices to communicate directly with each other.

A subnet (subnet), on the other hand, is the division of a larger network into smaller logical networks. It enables better organization and management of IP addresses by grouping devices based on network requirements, security policies, or other factors.

Without proper routing between subnets, devices on one subnet cannot communicate directly with devices on the other subnet.

In our project 10.10.10.0/24 , 20.20.20.0/24 and 30.30.30.0/24 
are the subnets of our LAN.


### DNS

A Domain Name System (DNS) turns domain names into IP addresses that allow browsers to access websites and other internet resources. Every device on the Internet has an IP address that other devices can use to locate the device. Rather than memorizing a long list of IP addresses, people can simply enter the website name and DNS will get the IP address for them.

### HTTP

Hypertext Transfer Protocol (HTTP) is the foundation of the World Wide Web and is used to load web pages using hypertext links. HTTP is an application layer protocol designed to transfer information between networked devices and runs on top of other layers of the network protocol stack. A typical flow over HTTP involves a client machine making a request to a server and the server then sending a response message.
### Static IP

IP address means internet protocol address; An identifying number associated with a particular computer or computer network. When connected to the Internet, the IP address allows computers to send and receive information. Every device has its own unique IP address. In this project we will use IPv4 which is the 32 bit IP address.

There are four different types of IP addresses: public, private, static, and dynamic. Public and private indicates the location of the network while static and dynamic indicates the permanency of the IP Address.

A static IP address is the one that is created manually and does not change over time. But, when establishing a network suppose you have 200 computers. You'd have to configure all the IP addresses, subnet-masks, and default gateway. And also these configurations differs from one operating system to another. Below you can see how static IP configurations are made on different operating systems.

<!-- 
    IDS:
     metasploitable-static-ip-configuration
     windows-static-ip-configuration
     ubuntu-server-static-ip-configuration
  -->
#### Metasploitable Static IP Configuration

[![metasploitable-static][metasploitable-static]](https://github.com/alperrkilic/DHCP-FTP-Server-with-PFSense)


#### Windows Static IP Configuration

_Control Panel -> Network and Internet -> Network and Sharing Center_

[![windows-static][windows-static]](https://github.com/alperrkilic/DHCP-FTP-Server-with-PFSense)

_Note that default gateway should be PFSense in our case since we are using firewall (in our case 10.10.10.2)_

[![windows-static][windows-static-2]](https://github.com/alperrkilic/DHCP-FTP-Server-with-PFSense)


#### Ubuntu Server Static IP Configuration

_/etc/netplan/00-installer-config.yaml_

[![ubuntu-server-static][ubuntu-server-static]](https://github.com/alperrkilic/DHCP-FTP-Server-with-PFSense)

### Broadcasting

Broadcasting is a type of group communication in which a sender provides data to multiple receivers at the same time. This is a communication model where each sending device sends data to all other devices in the network area.

When your computer first connects to a Local Area Network (LAN), it does not have an IP address. It must connect to a Dynamic Host Configuration Protocol (DHCP) server to obtain an IP address. To do this, your computer must perform a broadcast to a private Broadcast IP address of 255.255.255.255; this essentially means that every machine on the LAN will receive your request for an IP address. The DHCP server will respond with an IP address to be assigned to your machine.

In our case we will specify the broadcast address of LAN's as 10.10.10.255, 20.20.20.255, 30.30.30.255 meaning that the machines on these subnets will broadcast for IP address


_Metasploitable machine Broadcasting for getting IP_

[![before-getting-ip][before-getting-ip]](https://github.com/alperrkilic/DHCP-FTP-Server-with-PFSense)

_Refreshing networking service to get IP_

   ```sh
    /etc/init.d/networking restart
   ```


[![getting-ip][getting-ip]](https://github.com/alperrkilic/DHCP-FTP-Server-with-PFSense)

_Metasploitable machine after getting its IP from DHCP Server_

[![after-getting-ip][after-getting-ip]](https://github.com/alperrkilic/DHCP-FTP-Server-with-PFSense)

### DHCP

Dynamic Host Configuration Protocol (DHCP) is a network protocol used to automate the process of configuring devices on IP networks. In this project, we will use DHCP relay on PFSense Firewall since broadcasting is done only within the subnet, we have to indicate the server machine as distributor so that the other machines can get their IP's.

[![dhcp_server_running][dhcp_server_running]](https://github.com/alperrkilic/DHCP-FTP-Server-with-PFSense)


### Router

A router is a device that connects two or more packet switched networks or subnets. Layer 3 switch's can also act as routers.

One of the primary jobs of a router is to assign IP addresses to the computers on a home network. The router has a “pool” of IP addresses that it keeps track of. When a computer connects to it and asks for an IP address, the router picks an IP address from the pool and assigns it to the computer. The router makes sure that two computers are not assigned the same IP address. This process of computers asking for an IP address from the router is called “dynamic” IP address assignment. It uses a network protocol called DHCP (Dynamic Host Configuration Protocol).


[![router][router]](https://github.com/alperrkilic/DHCP-FTP-Server-with-PFSense)


### Switch

A network switch is a physical device that operates at the Data Link layer -- Layer 2 of the Open Systems Interconnect (OSI) model. It receives packets sent by devices connected to physical ports and forwards them to devices. intended to reach the packets. Switches can also operate at the Network Layer (Layer 3) where routing occurs. In summary, the switch forwards packets to the devices that the packets are intended to send and connects the local devices with the router.

[![switch_vs_router][switch_vs_router]](https://github.com/alperrkilic/DHCP-FTP-Server-with-PFSense)


_Difference between switch and router._

### Gateway

A gateway is a node in a computer network that provides an important stopping point for data to or from other networks. In this project, gateways are 10.10.10.2, 20.20.20.2, and 30.30.30.2 which are the IP's of the LAN networks.

If we compare the router and the gateway in simple terms, a router is a type of gateway that focuses specifically on routing network traffic. However, the Gateway can also refer to other types of devices that act as entry points between networks, such as firewall gateways or proxy servers.

[![gateway][gateway]](https://github.com/alperrkilic/DHCP-FTP-Server-with-PFSense)

### FTP

The term file transfer protocol (FTP) refers to a process that involves transferring files between devices over a network. The process works when one party allows the other to send or receive files over the Internet. In our project, Ubuntu Server (30.30.30.3) will be our FTP server where we upload or download files

[![ftp][ftp]](https://github.com/alperrkilic/DHCP-FTP-Server-with-PFSense)

_Connecting via FTP to Ubuntu Server_

[![ftp_send][ftp_send]](https://github.com/alperrkilic/DHCP-FTP-Server-with-PFSense)

_Sending file through FTP_


### TCP Handshake

The Three-Way Handshake or TCP 3-way handshake is a process used to establish a connection between a server and a client in a TCP/IP network. It is a three-step process that requires both the client and server to exchange synchronization and acknowledgment packets before the actual data communication process begins.


[![tcp_handshake][tcp_handshake]](https://github.com/alperrkilic/DHCP-FTP-Server-with-PFSense)


_TCP Handshake Scheme_
