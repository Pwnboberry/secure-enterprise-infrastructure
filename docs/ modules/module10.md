# Модуль 10. Автоматизация администрирования (PowerShell и Bash)

## Цель

Автоматизировать типовые задачи администрирования с помощью PowerShell и Bash:

- автоматическое создание пользователей Active Directory из CSV-файла;
- автоматическая проверка состояния доменной инфраструктуры на Ubuntu.

---

## Выполненные действия

### 1. Автоматизация создания пользователей Active Directory

На контроллере домена была создана директория для хранения скриптов:

```powershell
New-Item -ItemType Directory -Path "C:\Scripts"
```
![](https://github.com/Pwnboberry/secure-enterprise-infrastructure/blob/main/screenshots/module_10/создаем%20директорию.png)

---

### 2. Подготовка CSV-файла

Создан файл `users.csv`, содержащий сведения о пользователях:

| Имя | Фамилия | Логин | Подразделение |
|------|---------|--------|---------------|
| Maria | Sidorova | maria | IT |
| Alexey | Smirnov | alexey | HR |
| Olga | Kuznetsova | olga | Managers |

![](https://github.com/Pwnboberry/secure-enterprise-infrastructure/blob/main/screenshots/module_10/CSV-файл%20с%20пользователями.png)

Файл использовался как источник данных для автоматического создания учетных записей.

---

### 3. Созданиескрипта

Разработан скрипт `CreateUsers.ps1`, который:

- импортирует пользователей из CSV;
- создаёт учетные записи Active Directory;
- назначает пароль;
- включает учетную запись;
- помещает пользователя в соответствующее подразделение (OU);
- выводит информацию о результате выполнения.

![](https://github.com/Pwnboberry/secure-enterprise-infrastructure/blob/main/screenshots/module_10/СКРИПТ%20(НА%20WIN-SRV).png)

Запуск выполнялся командой:

```powershell
Set-ExecutionPolicy Bypass -Scope Process -Force
C:\Scripts\CreateUsers.ps1
```

После выполнения были автоматически созданы новые пользователи в соответствующих OU.

![](https://github.com/Pwnboberry/secure-enterprise-infrastructure/blob/main/screenshots/module_10/работа%20СКРИПТ%20(НА%20WIN-SRV).png)

---

### 4. Создание Bash-скрипта

На сервере Ubuntu разработан скрипт `check_domain.sh`.

Скрипт автоматически проверяет:

- подключение Ubuntu к домену;
- состояние службы Winbind;
- доступность доменных пользователей;
- корректность DNS-разрешения домена.

![](https://github.com/Pwnboberry/secure-enterprise-infrastructure/blob/main/screenshots/module_10/СКРИПТ%20(НА%20UBUNTU-SRV).png)

Скрипт получил права на выполнение:

```bash
sudo chmod +x /usr/local/bin/check_domain.sh
```

Запуск выполнялся командой:

```bash
sudo /usr/local/bin/check_domain.sh
```

---

### 5. Проверка работы

После запуска Bash-скрипта были успешно проверены:

- подключение к домену `company.local`;
- работа службы Winbind;
- доступность пользователей Active Directory;
- корректность DNS-настроек.

![](https://github.com/Pwnboberry/secure-enterprise-infrastructure/blob/main/screenshots/module_10/работа%20СКРИПТ%20(НА%20UBUNTU-SRV).png)

---

## Использованные технологии

`PowerShell` · `Bash` · `Active Directory` · `CSV` · `Winbind` · `Realmd` · `DNS` · `Samba`

---

#### Результат

В ходе выполнения модуля были автоматизированы типовые задачи администрирования инфраструктуры.

PowerShell-скрипт позволяет автоматически создавать пользователей Active Directory на основе CSV-файла, что значительно сокращает время массового создания учетных записей.

Bash-скрипт предназначен для быстрой диагностики состояния Linux-сервера, подключенного к домену, и позволяет оперативно проверить основные компоненты доменной инфраструктуры.

Оба сценария демонстрируют применение средств автоматизации при администрировании корпоративной сети.

### ✅ Модуль 10 выполнен!

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
- [Модуль 9: Резервное копирование](./module9.md) 
- [Модуль 10: Скрипты автоматизации](./module10.md) ← **Ты здесь**
