# HQ Edge Router 1 Configuration

## Basic Global Configuration:
***Past in Global Configuration Mode***

```plaintext
hostname COMCAST_ISP_R1
!
username ansible privilege 15 secret cisco
username admin privilege 15 secret cisco123
!
enable secret cisco
!
service password-encryption
!
ip domain-name comcast.net
!
crypto key generate rsa modulus 1024
!
banner login ^C
************************************************************************
*                          Welcome to COMCAST-ISP                      *
*            Authorized Access Only. All Activities Monitored.         *
*       Unauthorized access will be prosecuted to the fullest extent   *
*                       of the law. Proceed with caution.              *
************************************************************************
^C
!
banner exec ^C
************************************************************************
*                          Welcome to COMCAST-ISP                      *
*                  You are now in EXEC mode. Happy networking!         *
************************************************************************
^C
!

!
!
line console 0
 logging synchronous
 exec-timeout 5 0
 privilege level 15
 password cisco
 login

line vty 0 4
 logging synchronous
 exec-timeout 5 0
 privilege level 15
 password cisco
 login
 transport input ssh

interface e1/3
 description ***Internet WAN***
 ip address dhcp
 ip nat outside
 no shutdown
 exit

interface range e0/0-1
 shutdown
 exit

interface range e1/0-2
 shutdown
 exit

end
wr
```

## Verify Commands
***Past in exec mode***

```plaintext
show running-config
!
!
show ip interface brief
```
## IP-Settings
Configure the ISP router with the following ip-addressing

```bash
| Host     | Interface | IP Address     | Subnet Mask | Connected to |   
|----------|-----------|----------------|-------------|--------------|
| ISP      | e0/0      | 50.100.150.1   | /30         | EDGE-R1      |   
| ISP      | e0/1      | 50.100.150.5   | /30         | EDGE-R2      |   
| ISP      | e0/2      | 50.100.151.1   | /30         | BR1-R        |  
| ISP      | e0/3      | 50.100.151.5   | /30         | BR2-R        |   
```
![isp-flow-chart](/assets/isp-flow.svg)
