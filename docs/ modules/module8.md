# Модуль 8. Настройка Firewall

## Цель

Настроить межсетевой экран на серверах Windows Server и Ubuntu для защиты инфраструктуры, разрешив только необходимые сетевые сервисы и заблокировав все остальные входящие соединения.

---

## Выполненные действия

### 1. Настройка Windows Firewall

На контроллере домена **WIN-SRV** был настроен Windows Firewall с использованием встроенных групп правил и дополнительных правил для необходимых служб.

![](https://github.com/Pwnboberry/secure-enterprise-infrastructure/blob/main/screenshots/module_08/правила%20для%20разрешения%20RDP.png)

Разрешены следующие сервисы:

- Remote Desktop (RDP)
- SMB (File Sharing)
- DNS
- DHCP
- ICMP (Ping)

Для всех профилей (Domain, Private, Public) оставлено стандартное правило:

- **Inbound connections — Block (default)**

Таким образом разрешены только необходимые подключения, остальные входящие соединения блокируются.

![](https://github.com/Pwnboberry/secure-enterprise-infrastructure/blob/main/screenshots/module_08/все%20праивла1.png)

---

### 2. Настройка nftables на Ubuntu

На сервере **ubuntu-srv** установлен пакет **nftables**.

```bash
sudo apt install nftables -y
```

![](https://github.com/Pwnboberry/secure-enterprise-infrastructure/blob/main/screenshots/module_08/Установи%20nftables.png)

Создан основной файл конфигурации `/etc/nftables.conf`.

![](https://github.com/Pwnboberry/secure-enterprise-infrastructure/blob/main/screenshots/module_08/базовый%20конфиг.png)

Настроены правила, разрешающие:

- SSH (22)
- Samba (TCP 139, 445)
- NetBIOS (UDP 137, 138)
- DNS (53)
- Kerberos (88, 464)
- ICMP (Ping)

Политики безопасности:

- Input — **drop**
- Forward — **drop**
- Output — **accept**

После настройки сервис был включён и запущен:

```bash
sudo systemctl enable nftables
sudo systemctl start nftables
```
Проверка конфигурации:

```bash
sudo nft list ruleset
```

![](https://github.com/Pwnboberry/secure-enterprise-infrastructure/blob/main/screenshots/module_08/Включи%20и%20запусти%20nftables.png)

---

### 3. Проверка работоспособности

После применения правил была выполнена проверка сетевого взаимодействия между серверами.

Проверено:

- успешный обмен ICMP-пакетами между Windows Server и Ubuntu;
- доступ к общей папке Samba;
- подключение по SSH к серверу Ubuntu;
- блокировка неразрешённых входящих подключений.

![](https://github.com/Pwnboberry/secure-enterprise-infrastructure/blob/main/screenshots/module_08/Войди%20как%20ivan%40company.local.png)

---

## Результаты проверки

| Проверка | Результат |
|----------|:---------:|
| ICMP (Ping) между серверами | ✅ |
| Доступ к Samba | ✅ |
| Подключение по SSH | ✅ |
| Блокировка неразрешённых портов | ✅ |

---

## Используемые технологии

`Windows Firewall` · `nftables` · `SMB` · `SSH` · `ICMP` · `Active Directory`

---

## Результат

В рамках модуля была реализована базовая защита сетевой инфраструктуры.

На контроллере домена Windows Firewall настроен с использованием встроенных правил для служб Active Directory и дополнительных правил для необходимых сервисов.

На сервере Ubuntu развёрнут **nftables**, разрешающий только необходимые сетевые подключения. Проверка подтвердила корректную работу разрешённых сервисов и блокировку неразрешённых входящих соединений.

### ✅ Модуль 8 выполнен!

## Навигация по проекту

- [Модуль 0: Подготовка инфраструктуры](./module0.md)
- [Модуль 1: Установка Active Directory](./module1.md) 
- [Модуль 2: Создание пользователей и групп](./module2.md) 
- [Модуль 3: Ввод Windows в домен](./module3.md)
- [Модуль 4: Подключение Ubuntu к домену](./module4.md) 
- [Модуль 5: Настройка Samba](./module5.md) 
- [Модуль 6: Групповые политики (GPO)](./module6.md) 
- [Модуль 7: Политика аудита](./module7.md) 
- [Модуль 8: Настройка Firewall](./module8.md) ← **Ты здесь**
- [Модуль 9: Резервное копирование](./module9.md) 
- [Модуль 10: Скрипты автоматизации](./module10.md) 
