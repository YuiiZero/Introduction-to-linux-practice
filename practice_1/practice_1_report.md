# Отчёт по практической работе 1 "Введение в Linux"

## Работу выполнил

- ФИО: Стяжкин РА
- Табельный номер: 561904
- Направление: ЯМИИ
- Группа: К3161
- Поток: 1.1

## Декларация использования ИИ

В процессе работы над проектом был использован ИИ в целях:

- Помощи разъяснения информации
- Помощи с примерами
- Помощи в самопроверке

## Артефакты

### Таблица

| Команда  | Назначение                           | Пример 1                                        | Пример 2                                    |
| -------- | ------------------------------------ | ----------------------------------------------- | ------------------------------------------- |
| hostname | Вывести имя хоста                    | ![hostname1](./practice_1_images/hostname1.png) |                                             |
| tty      | Вывести путь до терминала            | ![tty1](./practice_1_images/tty1.png)           |                                             |
| pwd      | Вывести текущую директорию           | ![pwd1](./practice_1_images/pwd1.png)           | ![pwd2](./practice_1_images/pwd2.png)       |
| whoami   | Вывести текущего пользователя        | ![whoami1](./practice_1_images/whoami1.png)     | ![whoami2](./practice_1_images/whoami2.png) |
| who      | Вывести всех пользователей           | ![who1](./practice_1_images/who1.png)           |                                             |
| date     | Вывести (установить) время           | ![date1](./practice_1_images/date1.png)         | ![date2](./practice_1_images/date2.png)     |
| ls       | Вывести файлы                        | ![ls1](./practice_1_images/ls1.png)             | ![ls2](./practice_1_images/ls2.png)         |
| mkdir    | Создать папку                        | ![mkdir1](./practice_1_images/mkdir1.png)       |                                             |
| touch    | Создать файл                         | ![touch1](./practice_1_images/touch1.png)       |                                             |
| cd       | Сменить рабочую директорию           | ![cd1](./practice_1_images/cd1.png)             | ![cd2](./practice_1_images/cd2.png)         |
| cp       | Скопировать файл                     | ![cp1](./practice_1_images/cp1.png)             | ![cp2](./practice_1_images/cp2.png)         |
| mv       | Перенести (переименовать) файл       | ![mv1](./practice_1_images/mv1.png)             | ![mv2](./practice_1_images/mv2.png)         |
| rm       | Удалить файл                         | ![rm1](./practice_1_images/rm1.png)             | ![rm2](./practice_1_images/rm2.png)         |
| rmdir    | Удалить пустую директорию            | ![rmdir1](./practice_1_images/rmdir1.png)       | ![rmdir2](./practice_1_images/rmdir2.png)   |
| find     | Вывести иерархию файлов              | ![find1](./practice_1_images/find1.png)         |                                             |
| grep     | Найти строку по шаблону              | ![grep](./practice_1_images/grep.png)           |                                             |
| cat      | Вывести объединённый текст из файлов | ![cat1](./practice_1_images/cat1.png)           |                                             |
| echo     | Вывести строку                       | ![echo1](./practice_1_images/echo1.png)         |                                             |

### Скрипт

**passport.sh**

```sh
#!/bin/bash

mkdir -p /home/user/PASSPORT /home/user/PASSPORT/log /home/user/PASSPORT/tmp
cd /home/user/PASSPORT

mkdir -p tmp

# .tmp file containing date and host
touch tmp/datehost.tmp

cat > tmp/datehost.tmp << QUIT
DATE: $(date)
HOST: $(hostname)
QUIT

# .tmp file containing user
touch tmp/user.tmp

cat > tmp/user.tmp << QUIT
CURRENT USER: $(whoami)

USERS:
$(who)
QUIT

# .tmp file containing working directory and all the files it inludes
touch tmp/files.tmp

cat > tmp/files.tmp << QUIT
WORKING DIRECTORY: $(pwd)

FILES:
$(ls -la)

HIERARCHY:
$(find .)
QUIT

# passport.txt contatins unified information from .tmp files
touch passport.txt

cat > passport.txt << QUIT
===DATE_AND_HOST===
$(cat tmp/datehost.tmp)

===USER_INFORMATION===
$(cat tmp/user.tmp)

===FILES_INFORMATION===
$(cat tmp/files.tmp)
QUIT

mkdir -p log

touch log/report.log

echo "Script was executed: $(date)" >> log/report.log

rm -r tmp
```

**запуск**

```bash
# Сделать исполняемым
user@debian:~$ chmod +x script_passport.sh

# Запустить
user@debian:~$ ./script_passport.sh
```

**passport.txt**

```txt
===DATE_AND_HOST===
DATE: Thu Sep 17 01:52:59 PM MSK 2026
HOST: debian

===USER_INFORMATION===
CURRENT USER: user

USERS:
user     seat0        2026-09-17 13:51
user     tty2         2026-09-17 13:51

===FILES_INFORMATION===
WORKING DIRECTORY: /home/user/PASSPORT

FILES:
total 20
drwxrwxr-x  4 user user 4096 Sep 17 13:52 .
drwx------ 20 user user 4096 Sep 17 13:52 ..
drwxrwxr-x  2 user user 4096 Sep 16 12:50 log
-rw-rw-r--  1 user user  625 Sep 16 13:02 passport.txt
drwxrwxr-x  2 user user 4096 Sep 17 13:52 tmp

HIERARCHY:
.
./tmp
./tmp/user.tmp
./tmp/datehost.tmp
./tmp/files.tmp
./passport.txt
./log
./log/report.log
```

**report.log**

```txt
Script was executed: Wed Sep 16 12:50:59 PM MSK 2026
Script was executed: Wed Sep 16 12:52:12 PM MSK 2026
Script was executed: Wed Sep 16 12:52:14 PM MSK 2026
Script was executed: Wed Sep 16 12:52:15 PM MSK 2026
Script was executed: Wed Sep 16 12:55:59 PM MSK 2026
Script was executed: Wed Sep 16 12:59:26 PM MSK 2026
Script was executed: Wed Sep 16 01:02:00 PM MSK 2026
Script was executed: Thu Sep 17 01:52:59 PM MSK 2026
```

## Вопросы и задания

1. Что произошло, когда вы применяли команду chmod, чтобы сделать файл
   исполняемым?
   `chmod +x` меняет не сам файл, а его права доступа. Если раньше они были, например `-rwxrw-r--`, то после `chmod +x` они становятся `-rwxrwxr-x`.
2. Для каких процессорных архитектур есть готовые дистрибутивы Debian?
   Debian поддерживает следующие архитектуры: amd64, i386, arm64, armhf, armel, mips64el, mipsel, ppc64el, s390x, riscv64.
3. Дистрибутив Linux Debian поставляется в нескольких режимах:
   - Netinstall - установка небольшого ISO с последующей выборочной дозагрузкой необходимых пакетов. Удобен для установки на обычный ПК или сервер и когда есть стабильный интернет. Большинство пакетов устанавливаются из репозитория по сети.
   - Live-image - ISO образ Debian для компактных носителей, типа Flashdrive или DVD. Изменения, внесённые в систему не сохраняются после перезагрузки. Удобен для проверки совместимости железа и для того, чтобы проверить, подходит ли тебе Debian перед установкой. Часть пакетов установлена из образа, а часть устанавливается из репозитория по сети.
   - Образа DVD - Содержит несколько DVD образов Debian. Установка через образы DVD не требует подключения к интернету. Удобен, когда слабый интернет или когда нужно загрузить Debian сразу на несколько устройств. Пакеты deb берутся напрямую из образов DVD
   - Cloud - предназначен специально для установки на VPS. Пакеты deb устанавливаются по сети. Базовая система уже находится в облачном образе; дополнительные покеты скачиваются из репозитория по сети.

   В чем разница этих поставок? Приведите примеры, когда удобно применять каждый из вариантов. Откуда берутся пакеты при установке?
