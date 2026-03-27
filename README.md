# Multi-VLAN Network Infrastructure & Services Lab

## Architecture du Réseau
Ce projet simule une infrastructure d'entreprise avec segmentation VLAN, agrégation de liens et services serveurs.

## Technologies Utilisées
* **Cisco Networking:** Inter-VLAN Routing (R1), EtherChannel LACP (SW1, SW2, SW3), VTP v3, Trunking 802.1Q.
* **Services:** Windows Server 2019 (DHCP/DNS), Ubuntu Server (Apache2/FTP).

## Aperçu du Lab
<img width="811" height="604" alt="lab" src="https://github.com/user-attachments/assets/a4ee5894-4d33-4a10-bf1a-4205d43e3c44" />
## Windows Server 2019 
# DHCP
<img width="1024" height="624" alt="4" src="https://github.com/user-attachments/assets/54deb540-3062-42c2-8f29-88fb6adebaab" />
<img width="816" height="210" alt="3" src="https://github.com/user-attachments/assets/15f2321a-f784-40e5-898f-e17ca1934170" />
<img width="747" height="166" alt="2" src="https://github.com/user-attachments/assets/6ec3fb40-35f3-4c9f-9127-9bd2aa51ac80" />
<img width="835" height="169" alt="1" src="https://github.com/user-attachments/assets/81c3683e-44a7-43e2-9b92-a4db2565fc8d" />
# DNS
<img width="767" height="570" alt="1" src="https://github.com/user-attachments/assets/b2eebf15-3bf5-4343-b659-4b0b4c5afc3d" />
## Linux Server Ubuntu
# Apache2 (HTTP)
<img width="730" height="531" alt="server web" src="https://github.com/user-attachments/assets/c256fdc9-a5dd-4940-bb73-a801f3110013" />
<img width="294" height="108" alt="text web" src="https://github.com/user-attachments/assets/14173326-cfe6-4fd9-a355-f8c355c80f08" />
# FTP 
## Config-R1

hostname R1
!
boot-start-marker
boot-end-marker
!
aqm-register-fnf
!
enable secret 5 $1$LFMg$MEw8xs8E76j.kmQ2n6siL0
!
no aaa new-model
no ip icmp rate-limit unreachable
!
no ip domain lookup
ip domain name ofppt.ma
ip cef
no ipv6 cef
!
multilink bundle-name authenticated
!
username mohamed privilege 15 secret 5 $1$8952$kfu/XzzRo5LKS.NN2PKU8/
!
redundancy
!
ip tcp synwait-time 5
ip ftp username ofppt
ip ftp password 123456
ip ssh version 2
!
interface FastEthernet0/0
 description LINK_TO_SW1
 no ip address
 duplex half
!
interface FastEthernet0/0.10
 encapsulation dot1Q 10
 ip address 192.168.10.1 255.255.255.0
 ip helper-address 192.168.1.253
 ip helper-address 192.168.1.250
!
interface FastEthernet0/0.20
 encapsulation dot1Q 20
 ip address 192.168.20.1 255.255.255.0
 ip helper-address 192.168.1.250
!
interface FastEthernet0/0.100
 encapsulation dot1Q 100 native
 ip address 192.168.1.1 255.255.255.0
!
interface FastEthernet2/0
 no ip address
 shutdown
 duplex half
!
interface FastEthernet3/0
 no ip address
 shutdown
 duplex auto
 speed auto
!
interface FastEthernet3/1
 no ip address
 shutdown
 duplex auto
 speed auto
!
interface GigabitEthernet4/0
 no ip address
 shutdown
 negotiation auto
!
interface Serial5/0
 no ip address
 shutdown
 serial restart-delay 0
!
interface Serial5/1
 no ip address
 shutdown
 serial restart-delay 0
!
interface Serial5/2
 no ip address
 shutdown
 serial restart-delay 0
!
interface Serial5/3
 no ip address
 shutdown
 serial restart-delay 0
!
interface Ethernet6/0
 no ip address
 shutdown
 duplex half
!
interface Ethernet6/1
 no ip address
 shutdown
 duplex half
!
interface Ethernet6/2
 no ip address
 shutdown
 duplex half
!
interface Ethernet6/3
 no ip address
 shutdown
 duplex half
!
ip forward-protocol nd
no ip http server
no ip http secure-server
!
no cdp log mismatch duplex
!
control-plane
!
mgcp behavior rsip-range tgcp-only
mgcp behavior comedia-role none
mgcp behavior comedia-check-media-src disable
mgcp behavior comedia-sdp-force disable
!
mgcp profile default
!
gatekeeper
 shutdown
!
line con 0
 exec-timeout 0 0
 privilege level 15
 logging synchronous
 stopbits 1
line aux 0
 exec-timeout 0 0
 privilege level 15
 logging synchronous
 stopbits 1
line vty 0 2
 login local
 transport input ssh
line vty 3 4
 login
 transport input all
!
end
R1#
## Config-sw1
[config sw1.txt](https://github.com/user-attachments/files/26309812/config.sw1.txt)
hostname SW1
!
boot-start-marker
boot-end-marker
!
logging discriminator EXCESS severity drops 6 msg-body drops EXCESSCOLL
logging buffered 50000
logging console discriminator EXCESS
enable secret 5 $1$4IWa$1bpCcrCdPNydtLzVqYkAB.
!
username mohamed secret 5 $1$xXhB$aF3PZYsHtOsMYVYujOFgH/
no aaa new-model
no ip icmp rate-limit unreachable
!
no ip cef
no ip domain-lookup
ip domain-name ofppt.ma
!
no ipv6 cef
!
spanning-tree mode pvst
spanning-tree extend system-id
!
vlan internal allocation policy ascending
!
ip tcp synwait-time 5
ip ftp username ofppt
ip ftp password 123456
ip ssh version 2
!
interface Port-channel1
 description Link_to_SW2
 switchport
 switchport trunk encapsulation dot1q
 switchport trunk native vlan 100
 switchport mode trunk
!
interface Port-channel2
 description Link_to_SW3
 switchport
 switchport trunk encapsulation dot1q
 switchport trunk native vlan 100
 switchport mode trunk
!
interface Ethernet0/0
 description Link_to R1
 switchport trunk encapsulation dot1q
 switchport trunk native vlan 100
 switchport mode trunk
 duplex auto
!
interface Ethernet0/1
 duplex auto
!
interface Ethernet0/2
 duplex auto
!
interface Ethernet0/3
 duplex auto
!
interface Ethernet1/0
 description Link_to_SRV(ubuntu)ftp/web
 switchport trunk encapsulation dot1q
 switchport trunk native vlan 100
 switchport mode trunk
 duplex auto
!
interface Ethernet1/1
 description Link_to_SRV(win2019)dhcp/dns
 switchport trunk encapsulation dot1q
 switchport trunk native vlan 100
 switchport mode trunk
 duplex auto
!
interface Ethernet1/2
 switchport access vlan 100
 switchport mode access
 duplex auto
!
interface Ethernet1/3
 switchport access vlan 100
 switchport mode access
 duplex auto
!
interface Ethernet2/0
 description Link_to_SW2
 switchport trunk encapsulation dot1q
 switchport trunk native vlan 100
 switchport mode trunk
 duplex auto
 channel-group 1 mode active
!
interface Ethernet2/1
 description Link_to_SW2
 switchport trunk encapsulation dot1q
 switchport trunk native vlan 100
 switchport mode trunk
 duplex auto
 channel-group 1 mode active
!
interface Ethernet2/2
 description Link_to_SW3
 switchport trunk encapsulation dot1q
 switchport trunk native vlan 100
 switchport mode trunk
 duplex auto
 channel-group 2 mode active
!
interface Ethernet2/3
 description Link_to_SW3
 switchport trunk encapsulation dot1q
 switchport trunk native vlan 100
 switchport mode trunk
 duplex auto
 channel-group 2 mode active
!
interface Ethernet3/0
 duplex auto
!
interface Ethernet3/1
 duplex auto
!
interface Ethernet3/2
 duplex auto
!
interface Ethernet3/3
 duplex auto
!
interface Ethernet4/0
 duplex auto
!
interface Ethernet4/1
 duplex auto
!
interface Ethernet4/2
 duplex auto
!
interface Ethernet4/3
 duplex auto
!
interface Ethernet5/0
 duplex auto
!
interface Ethernet5/1
 duplex auto
!
interface Ethernet5/2
 duplex auto
!
interface Ethernet5/3
 duplex auto
!
interface Serial6/0
 no ip address
 shutdown
 serial restart-delay 0
!
interface Serial6/1
 no ip address
 shutdown
 serial restart-delay 0
!
interface Serial6/2
 no ip address
 shutdown
 serial restart-delay 0
!
interface Serial6/3
 no ip address
 shutdown
 serial restart-delay 0
!
interface Serial7/0
 no ip address
 shutdown
 serial restart-delay 0
!
interface Serial7/1
 no ip address
 shutdown
 serial restart-delay 0
!
interface Serial7/2
 no ip address
 shutdown
 serial restart-delay 0
!
interface Serial7/3
 no ip address
 shutdown
 serial restart-delay 0
!
interface Vlan1
 no ip address
 shutdown
!
interface Vlan100
 ip address 192.168.1.2 255.255.255.0
!
ip default-gateway 192.168.1.1
!
ip forward-protocol nd
no ip http server
!
control-plane
!

line con 0
 exec-timeout 0 0
 privilege level 15
 logging synchronous
line aux 0
 exec-timeout 0 0
 privilege level 15
 logging synchronous
line vty 0 2
 login local
 transport input ssh
line vty 3 4
 login
 transport input all
!
end

SW1#sh int trunk

Port                Mode         Encapsulation  Status        Native vlan
Et0/0               on           802.1q         trunking      100
Et1/0               on           802.1q         trunking      100
Et1/1               on           802.1q         trunking      100
Po1                 on           802.1q         trunking      100
Po2                 on           802.1q         trunking      100

Port                Vlans allowed on trunk
Et0/0               1-4094
Et1/0               1-4094
Et1/1               1-4094
Po1                 1-4094
Po2                 1-4094

Port                Vlans allowed and active in management domain
Et0/0               1,10,20,100
Et1/0               1,10,20,100
Et1/1               1,10,20,100
Po1                 1,10,20,100
Po2                 1,10,20,100

Port                Vlans in spanning tree forwarding state and not pruned

Port                Vlans in spanning tree forwarding state and not pruned
Et0/0               1,10,20,100
Et1/0               1,10,20,100
Et1/1               1,10,20,100
Po1                 1,10,20,100
Po2                 1,10,20,100

SW1#sh etherchannel summary
Flags:  D - down        P - bundled in port-channel
        I - stand-alone s - suspended
        H - Hot-standby (LACP only)
        R - Layer3      S - Layer2
        U - in use      N - not in use, no aggregation
        f - failed to allocate aggregator

        M - not in use, no aggregation due to minimum links not met
        m - not in use, port not aggregated due to minimum links not met
        u - unsuitable for bundling
        d - default port

        w - waiting to be aggregated
Number of channel-groups in use: 2
Number of aggregators:           2

Group  Port-channel  Protocol    Ports
------+-------------+-----------+-----------------------------------------------
1      Po1(SU)         LACP      Et2/0(P)       Et2/1(P)
2      Po2(SU)         LACP      Et2/2(P)       Et2/3(P)

SW1#sh vtp status
VTP Version                     : 3 (capable)
Configuration Revision          : 6
Maximum VLANs supported locally : 1005
Number of existing VLANs        : 8
VTP Operating Mode              : Server
VTP Domain Name                 : ofppt.ma
VTP Pruning Mode                : Disabled (Operationally Disabled)
VTP V2 Mode                     : Enabled
VTP Traps Generation            : Disabled
MD5 digest                      : 0x27 0x46 0x57 0x8D 0x96 0x19 0x04 0x3A
Configuration last modified by 0.0.0.0 at 2-22-26 17:04:24
Local updater ID is 0.0.0.0 (no valid interface found)
VTP version running             : 2
SW1#sh vtp password
VTP Password: 123

