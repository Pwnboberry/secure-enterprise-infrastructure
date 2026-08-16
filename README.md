#  Secure Active Directory Infrastructure

> **Развертывание защищённой корпоративной инфраструктуры на базе Windows Server 2022 и Ubuntu Server**

---

## Описание проекта

Проект демонстрирует создание защищённой корпоративной инфраструктуры с использованием **Active Directory**, **DNS**, **DHCP**, **Samba**, **Winbind**, **Group Policy**, **Windows Firewall** и **nftables**.

Инфраструктура полностью развёрнута в виртуальной среде **VirtualBox** и включает взаимодействие Windows и Linux в едином домене.

---

# 🎯 Цели проекта

* Развернуть контроллер домена Active Directory
* Настроить службы DNS и DHCP
* Создать пользователей, группы и организационные подразделения
* Подключить Windows и Ubuntu к домену
* Настроить файловый сервер Samba
* Реализовать групповые политики безопасности (GPO)
* Настроить аудит событий безопасности
* Настроить межсетевые экраны Windows Firewall и nftables
* Реализовать резервное копирование
* Автоматизировать часть задач с помощью PowerShell и Bash

---

# 🖥 Используемые технологии

### Операционные системы

* Windows Server 2022
* Windows 10
* Ubuntu Server

### Сетевые сервисы

* Active Directory Domain Services
* DNS
* DHCP
* Kerberos
* Samba
* Winbind

### Безопасность

* Group Policy
* Windows Firewall
* nftables
* Audit Policy
* LUKS
* IPsec

### Автоматизация

* PowerShell
* Bash

### Виртуализация

* Oracle VirtualBox

---

# Реализованный функционал

* ✔ Развернут контроллер домена Active Directory
* ✔ Настроены DNS и DHCP
* ✔ Созданы пользователи, группы и OU
* ✔ Windows-клиент введён в домен
* ✔ Ubuntu Server подключён к домену через Winbind
* ✔ Настроен файловый сервер Samba
* ✔ Реализованы групповые политики безопасности
* ✔ Настроены политики аудита
* ✔ Настроены Windows Firewall и nftables
* ✔ Реализовано резервное копирование
* ✔ Разработаны PowerShell и Bash скрипты автоматизации

---

# Модули проекта

| Модуль                    | Статус |
| ------------------------- | :----: |
| Подготовка инфраструктуры |    ✅   |
| Active Directory          |    ✅   |
| DNS                       |    ✅   |
| DHCP                      |    ✅   |
| Пользователи и группы     |    ✅   |
| Windows Client            |    ✅   |
| Ubuntu + Winbind          |    ✅   |
| Samba                     |    ✅   |
| Group Policy              |    ✅   |
| Audit Policy              |    ✅   |
| Firewall                  |    ✅   |
| Backup                    |    ✅   |
| Automation                |    ✅   |

---

# 📸 Скриншоты

Скриншоты каждого этапа находятся в каталоге

```
secure-enterprise-infrastructure/screenshots/
```

---

# Автор

**Pwnboberry**

GitHub: https://github.com/Pwnboberry

