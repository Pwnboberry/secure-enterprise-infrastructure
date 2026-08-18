# Модуль 6. Настройка групповых политик (GPO)

## Цель модуля

Настроить групповые политики Active Directory для ограничения действий пользователей домена. В ходе работы были реализованы политики, запрещающие использование командной строки, доступ к Панели управления, а также установка USB-накопителей.

---

## Выполненные задачи

- Создана политика **GPO_Restrictions**.
- Настроен запрет запуска командной строки (CMD).
- Настроен запрет открытия Панели управления.
- Создана политика **GPO_USB_Disable**.
- Настроен запрет установки съемных USB-устройств.
- Политики привязаны к организационным подразделениям (OU).
- Выполнено принудительное обновление групповых политик.
- Проверена работоспособность настроенных ограничений.

---

## Создание политики GPO_Restrictions

На контроллере домена **WIN-SRV** была открыта оснастка **Group Policy Management**.

Создан новый объект групповой политики:

- **GPO_Restrictions**

После создания политика была отредактирована.

![](https://github.com/Pwnboberry/secure-enterprise-infrastructure/blob/main/screenshots/module_06/создание%20GPO_Restrictions.png)

---

## Запрет использования командной строки

В редакторе групповых политик открыт раздел:

```text
User Configuration
└── Policies
    └── Administrative Templates
        └── System
            └── Prevent access to the command prompt
```

Параметр **Prevent access to the command prompt** переведен в состояние **Enabled**.

![](https://github.com/Pwnboberry/secure-enterprise-infrastructure/blob/main/screenshots/module_06/настройка%20запрета%20консоль.png)

После применения политики пользователи домена больше не могут запускать командную строку.

---

## Запрет доступа к Панели управления

В редакторе групповых политик открыт раздел:

```text
User Configuration
└── Policies
    └── Administrative Templates
        └── Control Panel
            └── Prohibit access to Control Panel and PC settings
```

Параметр **Prohibit access to Control Panel and PC settings** переведен в состояние **Enabled**.

![](https://github.com/Pwnboberry/secure-enterprise-infrastructure/blob/main/screenshots/module_06/ЗАПРЕТ%20панели.png)

После применения политики пользователям запрещено открывать Панель управления и параметры Windows.

---

## Создание политики GPO_USB_Disable

В оснастке **Group Policy Management** создан новый объект групповой политики:

- **GPO_USB_Disable**

Политика была отредактирована.

![](https://github.com/Pwnboberry/secure-enterprise-infrastructure/blob/main/screenshots/module_06/СОЗДАНИЕ%20usb%20otkl.png)

---

## 🔌 Запрет установки USB-устройств

В редакторе групповой политики открыт раздел:

```text
Computer Configuration
└── Policies
    └── Administrative Templates
        └── System
            └── Device Installation
                └── Device Installation Restrictions
                    └── Prevent installation of removable devices
```

Параметр **Prevent installation of removable devices** установлен в состояние **Enabled**.

![](https://github.com/Pwnboberry/secure-enterprise-infrastructure/blob/main/screenshots/module_06/Настройка%20отключение%20USB.png)

Данная политика запрещает установку съемных USB-накопителей.

---

## Привязка политик к подразделениям

Созданные политики были привязаны к организационным подразделениям домена:

- **IT**
- **HR**
- **Managers**

После привязки политики распространяются на пользователей указанных подразделений.

---

## Применение политик

На клиентском компьютере **win-pc01** выполнено принудительное обновление групповых политик.

Использовались команды:

```cmd
gpupdate /force
shutdown /r /t 0
```
![](https://github.com/Pwnboberry/secure-enterprise-infrastructure/blob/main/screenshots/module_06/ПРИМЕНИли%20ПОЛИТИКИ%20НА%20WIN-PC01.png)

После перезагрузки компьютера изменения вступили в силу.

---

## ✅ Проверка работы политик

Было выполнено тестирование созданных ограничений.

### Проверка запуска CMD

При попытке выполнить:

```cmd
cmd
```

система выводит сообщение:

> The command prompt has been disabled by your administrator.

![](https://github.com/Pwnboberry/secure-enterprise-infrastructure/blob/main/screenshots/module_06/запрет%20cmd%20done.png)

Это подтверждает корректную работу политики.

---

### Проверка Панели управления

При попытке открыть:

```text
control
```

![](https://github.com/Pwnboberry/secure-enterprise-infrastructure/blob/main/screenshots/module_06/запрет%20панель%20done%20.png)

доступ был запрещен согласно настроенной политике.

---

### Проверка ограничения USB

Политика запрета установки USB-накопителей была применена.

В виртуальной среде **VirtualBox** ограничение полностью проверить не удалось, поскольку эмуляция USB отличается от работы на физическом оборудовании.

В реальной инфраструктуре данная политика применяется штатно.

---

## Результаты выполнения

| Настройка | Результат |
|-----------|-----------|
| Запрет командной строки | ✅ Выполнено |
| Запрет Панели управления | ✅ Выполнено |
| Создание политики USB | ✅ Выполнено |
| Привязка GPO к OU | ✅ Выполнено |
| Обновление групповых политик | ✅ Выполнено |
| Проверка ограничений | ✅ Выполнено |

---

## 🔧 Используемые технологии

- Active Directory Domain Services
- Group Policy Management
- Group Policy Objects (GPO)
- Windows Server 2022
- Windows 10

---

## Итог модуля

В ходе выполнения модуля были успешно настроены групповые политики Active Directory. 
Пользователям домена запрещено использование командной строки и Панели управления. 
Также была создана политика, запрещающая установку съемных USB-устройств. 
Политики привязаны к организационным подразделениям и успешно применены на клиентском компьютере после обновления групповых политик.

## 🧭 Навигация по проекту

- [Модуль 0: Подготовка инфраструктуры](./module0.md) 
- [Модуль 1: Установка Active Directory](./module1.md) 
- [Модуль 2: Создание пользователей и групп](./module2.md) 
- [Модуль 3: Ввод Windows в домен](./module3.md) 
- [Модуль 4: Подключение Ubuntu к домену](./module4.md) 
- [Модуль 5: Настройка Samba](./module5.md) 
- [Модуль 6: Групповые политики (GPO)](./module6.md) ← **Ты здесь**
- [Модуль 7: Политика аудита](./module7.md) *(в разработке)*
- [Модуль 8: Настройка Firewall](./module8.md) *(в разработке)*
- [Модуль 9: Резервное копирование](./module9.md) *(в разработке)*
- [Модуль 10: Скрипты автоматизации](./module10.md) *(в разработке)*
