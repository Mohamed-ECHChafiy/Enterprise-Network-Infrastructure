
### Linkedin : www.linkedin.com/in/mohamed-ech-chafiy
# Architecture du Réseau
Ce projet simule une infrastructure d'entreprise avec segmentation VLAN, agrégation de liens et services serveurs.

## Technologies Utilisées
* **Cisco Networking:** Inter-VLAN Routing (R1), EtherChannel LACP (SW1, SW2, SW3), VTP v2, Trunking 802.1Q.
* **Services:** Windows Server 2019 (DHCP/DNS), Ubuntu Server (Apache2/VCftpd).

## Aperçu du Lab
<img width="811" height="604" alt="lab" src="https://github.com/user-attachments/assets/a4ee5894-4d33-4a10-bf1a-4205d43e3c44" />

# Windows Server 2019

<img width="1024" height="624" alt="4" src="https://github.com/user-attachments/assets/54deb540-3062-42c2-8f29-88fb6adebaab" />
<img width="669" height="433" alt="1" src="https://github.com/user-attachments/assets/68b1ae32-02bd-4391-a659-a6676601ebd2" />
<img width="456" height="412" alt="test ping1" src="https://github.com/user-attachments/assets/d998e1cd-9449-4d99-977c-36aefc222206" />
<img width="507" height="416" alt="test ping vlans" src="https://github.com/user-attachments/assets/4d546156-fa9a-4aa4-81de-c32a13f83126" />

## DHCP

<img width="721" height="98" alt="6" src="https://github.com/user-attachments/assets/d9087d58-08fe-4c6c-85cc-a7269269b637" />
<img width="816" height="210" alt="3" src="https://github.com/user-attachments/assets/15f2321a-f784-40e5-898f-e17ca1934170" />
<img width="747" height="166" alt="2" src="https://github.com/user-attachments/assets/6ec3fb40-35f3-4c9f-9127-9bd2aa51ac80" />
<img width="835" height="169" alt="1" src="https://github.com/user-attachments/assets/81c3683e-44a7-43e2-9b92-a4db2565fc8d" />


## DNS
<img width="775" height="247" alt="8" src="https://github.com/user-attachments/assets/82debe99-c499-4e9c-816c-edc4cd58e22d" />
<img width="767" height="570" alt="1" src="https://github.com/user-attachments/assets/b2eebf15-3bf5-4343-b659-4b0b4c5afc3d" />

# Linux Server Ubuntu
## Apache2 (HTTP)
<img width="730" height="531" alt="server web" src="https://github.com/user-attachments/assets/c256fdc9-a5dd-4940-bb73-a801f3110013" />
<img width="294" height="108" alt="text web" src="https://github.com/user-attachments/assets/a9538e64-58b0-47f5-a153-1f15ec2b2a60" />

## VSftpd

<img width="804" height="292" alt="2" src="https://github.com/user-attachments/assets/01c4e7f5-7389-4753-87a8-8d57a2ba80ba" />
<img width="398" height="98" alt="1" src="https://github.com/user-attachments/assets/cbc7f5bc-49c6-407c-9f57-490d912c5cbe" />

# Config-R1

<img width="330" height="480" alt="R1" src="https://github.com/user-attachments/assets/5b8c26cb-3f5a-4fe5-8d1d-a689112d376b" />

 [config-R1.txt](https://github.com/user-attachments/files/26323288/config-R1.txt)

# Config-SW1

[config sw1.txt](https://github.com/user-attachments/files/26309965/config.sw1.txt)

# Config-SW2

[config-sw2.txt](https://github.com/user-attachments/files/26309972/config-sw2.txt)

# Config-SW3

[config-sw3.txt](https://github.com/user-attachments/files/26309973/config-sw3.txt)

# TEST dhcp/ping/web/ftp

## VLAN 10 (IT)

### PC1
<img width="447" height="497" alt="vpc1" src="https://github.com/user-attachments/assets/96d34934-8a7d-417a-bbfb-48554e3ecf9d" />

### PC2 (kali)
<img width="647" height="183" alt="ifconfig" src="https://github.com/user-attachments/assets/f27861f9-62f9-43e5-b05b-019d5adc13db" />
<img width="525" height="535" alt="test ping kali" src="https://github.com/user-attachments/assets/98a82366-86dd-4312-b5a3-ab60abe95bbd" />
<img width="1159" height="644" alt="test web kal" src="https://github.com/user-attachments/assets/da02d0c2-13f8-4632-9ca9-b29b6fe79306" />
<img width="594" height="335" alt="3" src="https://github.com/user-attachments/assets/9f34c4c7-aa95-47e8-a478-1b29aa4604a1" />

## VLAN 20 (DEV)

### PC1

<img width="447" height="495" alt="vpc2" src="https://github.com/user-attachments/assets/06d55a85-5a2f-41ba-ba49-7d78130da25d" />

### PC2 (win-7)
<img width="643" height="370" alt="pc win7" src="https://github.com/user-attachments/assets/249192b1-2e3f-47b5-8100-9e388cf64c51" />
<img width="447" height="480" alt="test ping win7" src="https://github.com/user-attachments/assets/02108b24-ad65-4c08-9041-38e5c0e37e06" />
<img width="578" height="602" alt="test web win7" src="https://github.com/user-attachments/assets/0ba47956-71d3-4f57-b1c8-3029b8a82c6a" />
<img width="668" height="373" alt="4" src="https://github.com/user-attachments/assets/8aa90917-73b7-4e7a-8143-3687e5dbb395" />




