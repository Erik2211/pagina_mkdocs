**Unitat 01 - DHCP** 

Maite Martí 

![](Aspose.Words.7e061984-b0b2-4bc8-9099-6638129d80a3.001.png) Unitat1–DHCP Curso2021-2022![](Aspose.Words.7e061984-b0b2-4bc8-9099-6638129d80a3.002.png)

**UNIT 1 ![](Aspose.Words.7e061984-b0b2-4bc8-9099-6638129d80a3.003.png)**

![](Aspose.Words.7e061984-b0b2-4bc8-9099-6638129d80a3.004.png)

**What is DHCP and How DHCP Works? (DHCP Fundamentals Explained)** 

Computer networks can be of any form like a LAN, WAN etc. If you are connected to a local LAN or an internet connection, the IP addresses form the basis of communication over computer networks. An IP address is the identity of a host or a computer device while connected to any network. 

In most of the cases when you connect your computer to a LAN or internet, you’ll notice that the IP address and other information like subnet mask etc are assigned to your computer automatically. Have you ever thought about how this happens? Well, in this article we will understand the concept of DHCP that forms the basis of this functionality. 

**1.- What is DHCP?** 

DHCP stands for Dynamic Host Configuration Protocol. 

As the name suggests, DHCP is used to control the network configuration of a host through a remote server. DHCP functionality comes installed as a default feature in most of the contemporary operating systems. DHCP is an excellent  alternative  to  the  time-consuming  manual  configuration  of network settings on a host or a network device. 

DHCP works on a client-server model. Being a protocol, it has it’s own set of messages that are exchanged between client and server. 

Understanding DHCP helps in debugging many network related problems. 

Read  our  articles  on  wireshark  and  Journey  of  a  packet  on  network  to enhance your understanding on network and network debugging tools. 

In the next section, we will cover the working of this protocol. 

**2. -How DHCP Works?** 

Before learning the process through which DHCP achieves it’s goal, we first have to understand the different messages that are used in the process. 

1. **DHCPDISCOVER** 

It  is  a  DHCP  message  that  marks  the  beginning  of  a  DHCP  interaction between client and server. This message is sent by a client (host or device connected to a network) that is connected to a local subnet. It’s a broadcast message that uses 255.255.255.255 as destination IP address while the source IP address is 0.0.0.0 

2. **DHCPOFFER** 

It is DHCP message that is sent in response to DHCPDISCOVER by a DHCP server to DHCP client. This message contains the network configuration settings for the client that sent the DHCPDISCOVER message. 

3. **DHCPREQUEST** 

This DHCP message is sent in response to DHCPOFFER indicating that the client has accepted the network configuration sent in DHCPOFFER message from the server. 

4. **DHCPACK** 

This message is sent by the DHCP server in response to DHCPREQUEST recieved from the client. This message marks the end of the process that started  with  DHCPDISCOVER.  The  DHCPACK  message  is  nothing  but  an acknowledgement by the DHCP server that authorizes the DHCP client to start  using  the  network  configuration  it  received  from  the  DHCP  server earlier. 

5. **DHCPNAK** 

This  message  is  the  exact  opposite  to  DHCPACK  described  above.  This message is sent by the DHCP server when it is not able to satisfy the DHCPREQUEST message from the client. 

6. **DHCPDECLINE** 

This message is sent from the DHCP client to the server in case the client finds that the IP address assigned by DHCP server is already in use. 

7. **DHCPINFORM** 

This  message  is  sent  from  the  DHCP  client  in  case  the  IP  address  is statically  configured  on  the  client  and  only  other  network  settings  or configurations are desired to be dynamically acquired from DHCP server. 

8. **DHCPRELEASE** 

This message is sent by the DHCP client in case it wants to terminate the lease of network address it has be provided by DHCP server. 

![](Aspose.Words.7e061984-b0b2-4bc8-9099-6638129d80a3.005.png)

Now as we know about the various DHCP messages, it’s time to go through the the complete DHCP process to give a better Idea of how DHCP works. Note that the steps mentioned below assume that DHCP functionality is enabled by default on the client side. 

Here are the steps : 

- **Step  1:**  When  the  client  computer  (or  device)  boots  up  or  is connected to a network, a DHCPDISCOVER message is sent from the client to the server. As there is no network configuration information on the client so the message is sent with 0.0.0.0 as source address and 255.255.255.255 as destination address. If the DHCP server is on local subnet then it directly receives the message or in case it is on different subnet then a relay agent connected on client’s  subnet is used to pass on the request to DHCP server. The transport protocol used for this message is UDP and the port number used is 67. The client enters the initializing stage during this step. 
- **Step 2:** When the DHCP server receives the DHCPDISCOVER request message  then  it  replies  with  a  DHCPOFFER  message.  As  already explained,  this  message  contains  all  the  network  configuration settings required by the client. For example, the yaddr field of the message will contain the IP address to be assigned to client. Similarly the the subnet mask and gateway information is filled in the options field. Also, the server fills in the client MAC address in the chaddr field.  This  message  is  sent  as  a  broadcast  (255.255.255.255) message for the client to receive it directly or if DHCP server is in different subnet then this message is sent to the relay agent that takes care of whether the message is to be passed as unicast or broadcast. In this case also, UDP protocol is used at the transport layer with destination port as 68. The client enters selecting stage during this step 
- **Step  3:**  The  client  forms  a  DHCPREQUEST  message  in  reply  to DHCPOFFER message and sends it to the server indicating it wants to accept the network configuration sent in the DHCPOFFER message. If there were multiple DHCP servers that received DHCPDISCOVER then client could receive multiple DHCPOFFER messages. But, the client replies  to  only  one  of  the  messages  by  populating  the  server identification field with the IP address of a particular DHCP server. All the messages from other DHCP servers are implicitly declined. The DHCPREQUEST  message  will  still  contain  the  source  address  as 
  - as the client is still not allowed to use the IP address passed to  it  through  DHCPOFFER  message.  The  client  enters  requesting stage during this step. 
- **Step 4:** Once the server receives DHCPREQUEST from the client, it sends the DHCPACK message indicating that now the client is allowed to use the IP address assigned to it. The client enters the bound state during this step. 

**3.- The Concept of Lease** 

With all the necessary information on how DHCP works, one should also know that the IP  address assigned by DHCP server to DHCP client is on a lease. After the lease expires the DHCP server is free to assign the same IP address to any other host or device requesting for the same. For example, keeping lease time 8-10 hours is helpful in case of PC’s that are shut down at the end of the day.  So, lease has to be renewed from time to time. The DHCP client tries to renew the lease after half of the lease time has expired. This is done by the exchange of DHCPREQUEST and DHCPACK messages. While doing all this, the client enters the renewing stage. 

**4.- How To Set Up A DHCP Server For Your LAN**  

This tutorial describes how to set up a DHCP server (ISC-DHCP) for your local network. DHCP is short for "Dynamic Host Configuration Protocol", it's a protocol that handles the assignment of IP addresses, subnet masks, default routers, and other  IP  parameters  to  client  PCs  that  don't  have  a  static  IP  address.  Such computers try to find a DHCP server in their local network which in turn assigns them an IP address, gateway, etc. so that they can connect to the internet or other computers from the local network. 

In this short guide I will show how to set up a simple DHCP server (ISC-DHCP) on a Ubuntu  system  whose  sole  purpose  is  to  assign  IP  adresses,  a  gateway,  DNS servers, etc. to client computers from the local network that don't have a static IP address. You can use such a DHCP server in your home network, your office, etc., for example if your router doesn't come with a built-in DHCP server. If you set up such a DHCP server, please make sure you don't already have another one in your LAN as this might result in conflicts.  

**4.1- Preliminary Note** 

This is the current situation: 

- I'm  using  the  network  10.10.10.0,  subnetmask 255.255.255.0, broadcast address 10.10.10.255.
- My gateway to the internet is 10.10.10.2xx; on the gateway there's no DHCP server.
- My ISP told me the DNS servers I can use are 172.27.111.5 and 172.27.111.6
- I have a pool of 30 IP addresses (10.10.10.2 – 10.10.10.199) that can be dynamically assigned to client PCs and **that are not already in use**.

***4.2 HowtoinstallDHCPserver***

First of all, you need to install the DHCP server, which you can do by running the following command: sudo apt install isc-dhcp-server

***HowtoconfigureDHCPserver***

Once the installation is complete, you need to assign network interfaces on which the DHCP server will serve. To do so, edit the default configuration file of the DHCP server via any text editor (I've used vim for that purpose): 

sudo vim /etc/default/isc-dhcp-server

In the default configuration file edit the value of INTERFACESv4 and write the one you want the DHCP server to serve requests. 

INTERFACESv4="enps08" 

If you have more than one interface DHCP to serve add them inside the quotes separating with spaces. 

INTERFACESv4="enps0s8 enp0s3" 

Once the interface(s) is(are) assigned, you can proceed to DHCP server configuration. To configure the DHCP  server edit the /etc/dhcp/dhcpd.conf file via any text editor. To do so, type the command below: 

sudo vim /etc/dhcp/dhcpd.conf

Change the domain name and domain name servers (DNS) according to yours in the section mentioned below: 

- option definitions common to all supported networks...

` `option domain-name "your\_domain.com";

` `option domain-name-servers ns1.your\_domain.com, ns2.your\_domain.com;

If this DHCP server is the official DHCP server for the local network, the authoritative directive should be uncommented. 

authoritative;

For  an  internal  subnet  configuration  find  the  section  with  "A  slightly  different  configuration  for  an internal subnet." comment, uncomment all lines in the section and change the values according your needs. For example: 

subnet 10.10.10.0 netmask 255.255.255.0 { range 10.10.10.150 10.10.10.170; option domain-name-servers ns1.your\_domain.com; option domain-name "local.your\_domain.com"; option subnet-mask 255.255.255.0; 

option routers 10.10.10.2xx; 

option broadcast-address 10.10.10.255; default-lease-time 600; 

max-lease-time 7200; 

} 

In this configuration, we have mentioned the local domain name, DNS, IP range from which IPs will be assigned to clients, default and max lease times. 

Restart the DHCP server and it will start serve according to your configuration. To restart, type: systemctl restart isc-dhcp-server

***AssignfixedIPaddresstoclientwithspecificMACaddress***

If you want to assign specific IP address to specific client you can use client's MAC address to achieve that goal. This means that the fixed IP address will be assigned to the client whose MAC address is configured in the configuration file and it won't be assigned to any other client. 

To check MAC address on the client's machine run: ip a 

The output will look like the one below: 

eth0: <BROADCAST,MULTICAST,UP,LOWER\_UP> mtu 1500 qdisc fq\_codel state UP group default qlen 1000

` `link/ether 00:0c:29:39:c7:81 brd ff:ff:ff:ff:ff:ff

` `inet 10.10.2xx.210/24 brd 192.168.0.255 scope global dynamic eth0 

` `valid\_lft 73924sec preferred\_lft 73924sec

` `inet6  2600:3c01::f03c:91ff:fe62:5d78/64  scope  global  dynamic mngtmpaddr noprefixroute

` `valid\_lft 598sec preferred\_lft 298sec

` `inet6 fe80::f03c:91ff:fe62:5d78/64 scope link

` `valid\_lft forever preferred\_lft forever 

The underlined part is the MAC address of the mentioned network adapter. To assign fixed IP address to specific MAC address, edit the vim /etc/dhcp/dhcpd.conf file and add the following section (you must add different sections for different clients): 

host fixed-ip-client {

` `hardware ethernet 00:0c:29:39:c7:81;  fixed-address 10.10.10.250; 

` `} 

As you can notice we've given an IP address to the client out of the range that we configured to use the DHCP server. If you use an IP address within the IP range, DHCP server will skip that IP address to lease to clients dyamically and your IP range actually will be decreased by one IP address. 

After making changes in the configuration file, save it and restart the DHCP server to apply the changes. To restart type the following command: 

systemctl restart isc-dhcp-server

To  restart the  network  service  on  Ubuntu  machine  client  command  line  you  can  run  one  of  the following commands: 

sudo systemctl restart NetworkManager.service or 

sudo service network-manager restart

After network service restart, if you check network configuration with ifconfig or ip command, you will see output like the one below: 

eth0: <BROADCAST,MULTICAST,UP,LOWER\_UP> mtu 1500 qdisc fq\_codel state UP group default qlen 1000 

link/ether 00:0c:29:39:c7:81 brd ff:ff:ff:ff:ff:ff 

inet10.10.10.250/24 brd 10.10.10.255 scope global dynamic eth0 valid\_lft 73924sec preferred\_lft 73924sec 

inet6  2600:3c01::f03c:91ff:fe62:5d78/64  scope  global  dynamic mngtmpaddr noprefixroute 

valid\_lft 598sec preferred\_lft 298sec 

inet6 fe80::f03c:91ff:fe62:5d78/64 scope link 

valid\_lft forever preferred\_lft forever 

This exact output is from the client machine that we have configured to receive fixed IP address. As it's seen from output it received 10.10.10.250 IP address which we have set in /etc/dhcp/dhcpd.conf file on dhcp server. 

**4.4 How Can I See That My DHCP Server Is Working OK?** 

To see if your DHCP server is working as expected, boot another PC (Windows, Linux, MAC, ...) in your LAN that doesn't have a static IP address. Wait a few seconds, and in /var/log/syslog on the DHCP server you should see that the DHCP server  assigns  an  IP  address  to  your  PC.  For  example,  in  this  excerpt  of /var/log/syslog,  a  client  PC  named  matze  has  been  assigned  the  IP  address 192.168.88.209: 

Sep 19 16:01:26 server1 dhcpd: DHCPDISCOVER from 00:0c:76:8b:c4:16 via eth0 Sep 19 16:01:26 server1 dhcpd: DHCPOFFER on 10.10.10.250 to 00:0c:76:8b:c4:16 (matze) via eth0 

Sep 19 16:01:27 server1 dhcpd: DHCPDISCOVER from 00:0c:76:8b:c4:16 (matze) via eth0 

Sep 19 16:01:27 server1 dhcpd: DHCPOFFER on 10.10.10.250 to 00:0c:76:8b:c4:16 (matze) via eth0 

Sep 19 16:01:31 server1 dhcpd: DHCPDISCOVER from 00:0c:76:8b:c4:16 (matze) via eth0 

Sep 19 16:01:31 server1 dhcpd: DHCPOFFER on 10.10.10.250 to 00:0c:76:8b:c4:16 (matze) via eth0 

Sep 19 16:01:31 server1 dhcpd: Wrote 1 leases to leases file. 

Sep  19  16:01:31  server1  dhcpd:  DHCPREQUEST  for  10.10.10.250  from 00:0c:76:8b:c4:16 (matze) via eth0 

Sep 19 16:01:31 server1 dhcpd: DHCPACK on 10.10.10.250 to 00:0c:76:8b:c4:16 (matze) via eth0 

The  DHCP  server  writes  all  current  IP  address  "leases"  to  the  file /var/lib/dhcp3/dhcpd.leases so you should also find the lease there: 

vi /var/lib/dhcp3/dhcpd.leases ![](Aspose.Words.7e061984-b0b2-4bc8-9099-6638129d80a3.006.png)

- All times in this file are in UTC (GMT), not your local timezone.   This is ![](Aspose.Words.7e061984-b0b2-4bc8-9099-6638129d80a3.007.png)
- not a bug, so please don't ask about it.   There is no portable way to # store leases in the local timezone, so please don't request this as a # feature.    If  this  is  inconvenient  or  confusing  to  you,  we  sincerely  # apologize.   Seriously, though - don't ask. # The format of this file is documented in the dhcpd.leases(5) manual page. # This lease file was written by isc-dhcp-V3.0.1  lease 10.10.10.250{   starts 2 2006/09/19 14:01:31;   ends 3 2006/09/20 14:01:31;   binding state active;   next binding  state  free;    hardware  ethernet  00:0c:76:8b:c4:16;    uid "\001\000\014v\213\304\026";   client-hostname "matze"; } 

Have Fun! 
9
