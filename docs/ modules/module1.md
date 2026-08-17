# Модуль 1. Развёртывание доменной инфраструктуры

## Цель модуля

Развернуть базовую инфраструктуру Active Directory на базе Windows Server 2022, установить и настроить роли Active Directory Domain Services (AD DS), DNS и DHCP, создать домен `company.local` и подготовить сервер для дальнейшего подключения рабочих станций и Linux-сервера.

---

## Выполненные действия

### Установка ролей

На сервере **WIN-SRV** через **Server Manager** были установлены следующие роли:

- Active Directory Domain Services (AD DS);
- DNS Server;
- DHCP Server.

![](https://github.com/Pwnboberry/secure-enterprise-infrastructure/blob/main/screenshots/module_01/Установка%20и%20настройка%20ролей%20DONE.png)

После завершения установки сервер был подготовлен к повышению до контроллера домена.

---

### Создание домена Active Directory

Сервер был повышен до контроллера домена с созданием нового леса.

![](https://github.com/Pwnboberry/secure-enterprise-infrastructure/blob/main/screenshots/module_01/Авторизовали%20сервер%20в%20AD.png)

Параметры домена:

- Домен: `company.local`
- NetBIOS-имя: `COMPANY`

После установки сервер автоматически перезагрузился и начал выполнять функции контроллера домена.

---

### Настройка DNS

После создания домена автоматически появилась зона прямого просмотра `company.local`.

Дополнительно была создана зона обратного просмотра (Reverse Lookup Zone) для сети:

```
192.168.10.0/24
```
![](https://github.com/Pwnboberry/secure-enterprise-infrastructure/blob/main/screenshots/module_01/зона%20192.168.10.x%20Subnet.png)

![](https://github.com/Pwnboberry/secure-enterprise-infrastructure/blob/main/screenshots/module_01/_reverse_zone.png)

Также была создана PTR-запись для сервера:

| Имя | IP |
|-----|----|
| win-srv.company.local | 192.168.10.10 |

![](https://github.com/Pwnboberry/secure-enterprise-infrastructure/blob/main/screenshots/module_01/PTR-запись..png)

Это позволило выполнять как прямое, так и обратное разрешение DNS-имён.

---

### Настройка DHCP

DHCP-сервер был авторизован в Active Directory.

Создана область выдачи адресов:

| Параметр | Значение |
|----------|----------|
| Диапазон | 192.168.10.20 – 192.168.10.100 |
| Маска | 255.255.255.0 |
| DNS | 192.168.10.10 |
| Домен | company.local |

![](https://github.com/Pwnboberry/secure-enterprise-infrastructure/blob/main/screenshots/module_01/диапазоном%20адресов%20для%20выдачи%20клиентам%20от%20192.168.10.20%20до%20192.168.10.100.png)

Шлюз не настраивался, так как лабораторная сеть является полностью изолированной.

---

### Проверка работы DHCP

После перезагрузки рабочей станции **win-pc01** компьютер автоматически получил IP-адрес из созданной DHCP-области.

Команда

```cmd
ipconfig
```

подтвердила получение:

- IPv4-адреса из диапазона DHCP;
- DNS-сервера `192.168.10.10`.

![](https://github.com/Pwnboberry/secure-enterprise-infrastructure/blob/main/screenshots/module_01/nslookup%20company.local%20(2).png)

---

### Проверка работы DNS

Работа DNS была проверена как на Windows, так и на Ubuntu.

На Windows:

```cmd
nslookup company.local
```

На Ubuntu:

```bash
nslookup company.local 192.168.10.10
```

![](https://github.com/Pwnboberry/secure-enterprise-infrastructure/blob/main/screenshots/module_01/поиск%20домена%20с%20убунту.png)

Оба запроса успешно разрешили имя домена.

Также была проверена обратная зона:

```bash
nslookup 192.168.10.10 192.168.10.10
```

В результате была получена PTR-запись:

```
win-srv.company.local
```

---

## Результат

После выполнения модуля была полностью подготовлена доменная инфраструктура.

В результате:

- установлен контроллер домена Active Directory;
- создан домен `company.local`;
- настроен DNS-сервер с прямой и обратной зонами;
- настроен DHCP-сервер;
- рабочая станция автоматически получает IP-адрес;
- Windows и Ubuntu корректно используют DNS-сервер домена.

Данная инфраструктура будет использоваться в последующих модулях проекта для подключения рабочих станций, настройки Samba Active Directory, групповых политик, аудита безопасности и других компонентов корпоративной сети.

### ✅ Модуль 1 выполнен!

## 🧭 Навигация по проекту

- [Модуль 0: Подготовка инфраструктуры](./module0.md)
- [Модуль 1: Установка Active Directory](./module1.md) ← **Ты здесь**
- [Модуль 2: Создание пользователей и групп](./module2.md) *(в разработке)*
- [Модуль 3: Ввод Windows в домен](./module3.md) *(в разработке)*
- [Модуль 4: Подключение Ubuntu к домену](./module4.md) *(в разработке)*
- [Модуль 5: Настройка Samba](./module5.md) *(в разработке)*
- [Модуль 6: Групповые политики (GPO)](./module6.md) *(в разработке)*
- [Модуль 7: Политика аудита](./module7.md) *(в разработке)*
- [Модуль 8: Настройка Firewall](./module8.md) *(в разработке)*
- [Модуль 9: Резервное копирование](./module9.md) *(в разработке)*
- [Модуль 10: Скрипты автоматизации](./module10.md) *(в разработке)*

