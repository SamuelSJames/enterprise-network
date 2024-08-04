# HQ Edge Router 1 Configuration

## Basic Global Configuration:
***Past in Global Configuration Mode***

```plaintext
hostname HQ_EDGE_R1
!
username ansible privilege 15 secret cisco
username admin privilege 15 secret cisco123
!
enable secret cisco
!
service password-encryption
!
ip domain-name aminsurance.com
!
crypto key generate rsa modulus 1024
!
banner login ^C
************************************************************************
*                          Welcome to HQ_EDGE_R1                       *
*            Authorized Access Only. All Activities Monitored.         *
*       Unauthorized access will be prosecuted to the fullest extent   *
*                       of the law. Proceed with caution.              *
************************************************************************
^C
!
banner exec ^C
************************************************************************
*                          Welcome to HQ_EDGE_R1                       *
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
!
interface e0/0
 description ***Primary ISP***
 ip address 50.100.150.2 255.255.255.252
 ip nat outside
 no shut
 exit
!
interface e1/3.100
 description ***EDGE NETWORK***
 ip address 10.0.100.1 255.255.255.0
 ip nat inside
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
## IP-Settings:

```bash
| Host       | Interface | IP Address    | Subnet Mask      | Connected to |
|------------|-----------|---------------|------------------|--------------|
| HQ_EDGE_R1 | e0/0      | 50.100.150.2  | 255.255.255.252  | ISP          |
| HQ_EDGE_R1 | e1/3.100  | 10.0.100.1    | 255.255.255.0    | DIST-SW1     |
| HQ_EDGE_R1 | e1/3.101  | 10.0.101.1    | 255.255.255.0    | DIST-SW1     |
| HQ_EDGE_R1 | e1/3.160  | 10.0.160.1    | 255.255.255.0    | DIST-SW1     |

```
![flow](/assets/edger1-flow.svg)
