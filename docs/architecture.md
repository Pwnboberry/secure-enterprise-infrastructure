# Архитектура проекта

## Цель

Развернуть защищённую корпоративную инфраструктуру с использованием Windows Server и Ubuntu.

---

## Состав инфраструктуры

### WIN-SRV

- Windows Server 2022
- Active Directory
- DNS
- DHCP
- Group Policy
- Windows Firewall

IP:
192.168.10.10

---

### WIN-PC01

- Windows 10
- Член домена company.local

IP:
DHCP

---

### UBUNTU-SRV

- Ubuntu Server
- Samba
- Winbind
- SSH
- nftables

IP:
192.168.10.12

---

## Используемые сервисы

- Active Directory
- DNS
- DHCP
- SMB
- Kerberos
- SSH


![](https://github.com/Pwnboberry/secure-enterprise-infrastructure/blob/main/network-topology.png)
