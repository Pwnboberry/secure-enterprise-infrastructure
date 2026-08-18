# Модуль 0. Подготовка инфраструктуры

## Цель модуля

Создать виртуальную лабораторную среду для развёртывания корпоративной инфраструктуры с доменом `company.local` с использованием Windows Server 2022, Windows 10 и Ubuntu Server.

В рамках модуля была подготовлена базовая сеть, создана виртуальная среда и настроено взаимодействие между всеми узлами инфраструктуры.

---

## Архитектура лаборатории

Виртуальная инфраструктура состоит из трёх машин:

| Имя устройства | Операционная система | Назначение | IP-адрес |
|----------------|----------------------|------------|----------|
| `WIN-SRV` | Windows Server 2022 | Контроллер домена, DNS, DHCP | `192.168.10.10` |
| `WIN-PC01` | Windows 10 | Клиент домена | DHCP |
| `UBUNTU-SRV` | Ubuntu Server | Linux-сервер, Samba | `192.168.10.12` |

---

## Выполненные действия

### 1. Создание виртуальных машин

В среде виртуализации **Oracle VirtualBox** были созданы три виртуальные машины:

- `WIN-SRV` — серверная система Windows Server 2022;
- `WIN-PC01` — клиентская система Windows 10;
- `UBUNTU-SRV` — сервер Ubuntu Linux.

Для всех виртуальных машин выделены необходимые ресурсы для работы инфраструктурных сервисов.

---

### 2. Настройка внутренней сети

Для взаимодействия между виртуальными машинами была создана внутренняя сеть VirtualBox:
Network: intnet1
Subnet: 192.168.10.0/24


Все устройства были подключены к одной изолированной сети, что позволило им взаимодействовать между собой без доступа к внешней сети.

---

### 3. Настройка IP-адресации

## Настройка WIN-SRV (Windows Server 2022)
На серверных узлах были назначены статические IP-адреса:
WIN-SRV:
192.168.10.10
С помощью команды:

```bash
New-NetIPAddress -InterfaceAlias "Ethernet" -IPAddress 192.168.10.10 -PrefixLength 24
```

![](https://github.com/Pwnboberry/secure-enterprise-infrastructure/blob/main/screenshots/module_0/устаанвливаем%20айпи%20winsrv.png)

Также укажем DNS-сервером сам себя (127.0.0.1), так как на WIN-SRV будет установлена роль DNS.

```bash
Set-DnsClientServerAddress -InterfaceAlias "Ethernet" -ServerAddresses 127.0.0.1
```
### Изменение имени компьютера
С помощью команды:

```bash
Rename-Computer -NewName "WIN-SRV" -Restart
```

![](https://github.com/Pwnboberry/secure-enterprise-infrastructure/blob/main/screenshots/module_0/переименвываем%20пк.JPG)

## Настройка ubuntu-srv (Ubuntu Server)
UBUNTU-SRV:
192.168.10.12

```bash
sudo nano /etc/netplan/01-netcfg.yaml
```

![](https://github.com/Pwnboberry/secure-enterprise-infrastructure/blob/main/screenshots/module_0/Настройка%20сети%20(IP-адрес)%20ubuntu.JPG)

Настройка имени хоста:

```bash
sudo hostnamectl set-hostname ubuntu-srv
```

![](https://github.com/Pwnboberry/secure-enterprise-infrastructure/blob/main/screenshots/module_0/переименвываем%20пк%20ubuntu.JPG)

Настройка файла hosts:
Добавляем запись, чтобы Ubuntu знала, где находится контроллер домена:
```bash
192.168.10.10  win-srv.company.local  win-srv
192.168.10.12  ubuntu-srv.company.local  ubuntu-srv
```

![](https://github.com/Pwnboberry/secure-enterprise-infrastructure/blob/main/screenshots/module_0/Добавили%20записи%2C%20чтобы%20Ubuntu%20знала%2C%20где%20искать%20WIN-SRV%20и%20себя..JPG)

## Настройка win-pc01 (Windows 10 Pro)

На PC-01 Айпи будет выдан автоматически, благодаря настройке dhcp в будущем, но пока можно ввести вручную:

![](https://github.com/Pwnboberry/secure-enterprise-infrastructure/blob/main/screenshots/module_0/настройка%20адаптеров%20pc01.JPG)

Изменение имени компьютера:
```bash
Rename-Computer -NewName "win-pc01" -Restart
```

![](https://github.com/Pwnboberry/secure-enterprise-infrastructure/blob/main/screenshots/module_0/переименвываем%20пк%20pc01.JPG)

### ПРОВЕРКА СВЯЗИ МЕЖДУ МАШИНАМИ
На этом этапе WIN-SRV еще не контроллер домена, но пинг между машинами уже должен работать.

Выполняеи проверку доступности машин с помощью утилиты `ping`.  
Тестирование проводилось с каждой машины по направлению к остальным узлам сети.

| Откуда | Куда | IP-адрес | Команда | Ожидаемый результат |
|--------|------|----------|---------|----------------------|
| `WIN-SRV` | `ubuntu-srv` | `192.168.10.12` | `ping 192.168.10.12` | ✅ Успешный ответ |
| `win-pc01` | `WIN-SRV` | `192.168.10.10` | `ping 192.168.10.10` | ✅ Успешный ответ |
| `win-pc01` | `ubuntu-srv` | `192.168.10.12` | `ping 192.168.10.12` | ✅ Успешный ответ |
| `ubuntu-srv` | `WIN-SRV` | `192.168.10.10` | `ping 192.168.10.10` | ✅ Успешный ответ |
| `ubuntu-srv` | `win-pc01` | `192.168.10.11` | `ping 192.168.10.11` | ✅ Успешный ответ |

Скриншоты успешного пинга добавлены в раздел `screenshots/module_0`

**Результат:**  
Все машины успешно обнаруживают друг друга в сети. Связь между узлами работает корректно.

### ✅ Модуль 0 выполнен!

## 🧭 Навигация по проекту

- [Модуль 0: Подготовка инфраструктуры](./module0.md) ← **Ты здесь**
- [Модуль 1: Установка Active Directory](./module1.md) 
- [Модуль 2: Создание пользователей и групп](./module2.md) 
- [Модуль 3: Ввод Windows в домен](./module3.md) 
- [Модуль 4: Подключение Ubuntu к домену](./module4.md) 
- [Модуль 5: Настройка Samba](./module5.md) 
- [Модуль 6: Групповые политики (GPO)](./module6.md) 
- [Модуль 7: Политика аудита](./module7.md) *(в разработке)*
- [Модуль 8: Настройка Firewall](./module8.md) *(в разработке)*
- [Модуль 9: Резервное копирование](./module9.md) *(в разработке)*
- [Модуль 10: Скрипты автоматизации](./module10.md) *(в разработке)*
