# Модуль 9. Резервное копирование

## Цель

Настроить резервное копирование критически важных компонентов инфраструктуры:

- Active Directory на Windows Server;
- конфигурационных файлов на Ubuntu Server;
- автоматическое выполнение резервного копирования по расписанию.

---

## Выполненные действия

### 1. Установка Windows Server Backup

На контроллере домена **WIN-SRV** был установлен компонент **Windows Server Backup** через **Server Manager → Add Roles and Features**.

---
![](https://github.com/Pwnboberry/secure-enterprise-infrastructure/blob/main/screenshots/module_09/Установи%20Windows%20Server%20Backup.png)

### 2. Создание резервной копии System State

В Windows Server Backup была выполнена разовая резервная копия состояния системы (**System State**).

В состав резервной копии входят:

- Active Directory Domain Services;
- DNS Server;
- системный реестр;
- загрузочные файлы;
- конфигурация операционной системы.

Резервная копия была успешно создана.

![](https://github.com/Pwnboberry/secure-enterprise-infrastructure/blob/main/screenshots/module_09/бэкап%20делаеи.png)

---

### 3. Настройка автоматического резервного копирования

Через мастер **Backup Schedule** было настроено автоматическое выполнение резервного копирования.

Параметры:

- ежедневный запуск;
- резервное копирование System State;
- сохранение на локальный диск.

---
![](https://github.com/Pwnboberry/secure-enterprise-infrastructure/blob/main/screenshots/module_09/автоматический%20бэкап%20по%20расписанию.png)

### 4. Создание каталога резервных копий на Ubuntu

На сервере **ubuntu-srv** создан каталог:

```bash
sudo mkdir -p /backup
```

---

### 5. Создание скрипта резервного копирования

Создан скрипт:

```text
/usr/local/bin/backup_configs.sh
```
![](https://github.com/Pwnboberry/secure-enterprise-infrastructure/blob/main/screenshots/module_09/usrlocalbinbackup_configs.sh.png)

Скрипт выполняет:

- архивирование конфигурационных файлов;
- сохранение архива в каталог `/backup`;
- автоматическое удаление резервных копий старше 7 дней.

Архивируются следующие файлы:

- `/etc/samba/smb.conf`
- `/etc/sssd/sssd.conf`
- `/etc/krb5.conf`
- `/etc/hosts`
- `/etc/netplan/*.yaml`

---

### 6. Проверка работы скрипта

Скрипт был cделан исполняемым, а после запущен вручную:

```bash
sudo /usr/local/bin/backup_configs.sh
```

После выполнения в каталоге `/backup` появился архив с текущей датой и временем.

Проверка:

```bash
ls -la /backup/
```
![](https://github.com/Pwnboberry/secure-enterprise-infrastructure/blob/main/screenshots/module_09/Сделай%20скрипт%20исполняемым.png)

---

### 7. Настройка автоматического запуска через Cron

Для пользователя **root** было создано задание Cron:

```text
0 3 * * * /usr/local/bin/backup_configs.sh
```
![](https://github.com/Pwnboberry/secure-enterprise-infrastructure/blob/main/screenshots/module_09/автоматический%20бэкап%20через%20cron.png)

Скрипт автоматически запускается ежедневно в **03:00**.

Проверка:

```bash
sudo crontab -l
```

---

## Используемые технологии

- Windows Server Backup
- Active Directory
- Bash
- tar
- cron
- Linux

---

## Результат

В рамках модуля была реализована система резервного копирования для серверной инфраструктуры.

На контроллере домена настроено резервное копирование состояния системы (System State), обеспечивающее возможность восстановления Active Directory и системных служб.

На сервере Ubuntu реализован автоматизированный механизм резервного копирования конфигурационных файлов с использованием Bash-скрипта и планировщика Cron, 
что обеспечивает регулярное сохранение критически важных настроек системы.

### ✅ Модуль 9 выполнен!

## Навигация по проекту

- [Модуль 0: Подготовка инфраструктуры](./module0.md)
- [Модуль 1: Установка Active Directory](./module1.md)
- [Модуль 2: Создание пользователей и групп](./module2.md) 
- [Модуль 3: Ввод Windows в домен](./module3.md) 
- [Модуль 4: Подключение Ubuntu к домену](./module4.md) 
- [Модуль 5: Настройка Samba](./module5.md) 
- [Модуль 6: Групповые политики (GPO)](./module6.md) 
- [Модуль 7: Политика аудита](./module7.md) 
- [Модуль 8: Настройка Firewall](./module8.md) 
- [Модуль 9: Резервное копирование](./module9.md) ← **Ты здесь**
- [Модуль 10: Скрипты автоматизации](./module10.md) 
