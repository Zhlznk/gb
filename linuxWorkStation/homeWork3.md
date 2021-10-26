# Урок 3. Пользователи. Управление Пользователями и группами

## 1. Управление пользователями:

- a) создать пользователя, используя утилиту useradd;
```sh
~$ sudo useradd -m bogdan
[sudo] пароль для zhlznk: 
~$ sudo id bogdan
uid=1001(bogdan) gid=1001(bogdan) группы=1001(bogdan)
```

- b) удалить пользователя, используя утилиту userdel;

```sh
~$ sudo userdel -r bogdan
~$ sudo id bogdan
id: «bogdan»: такого пользователя нет
```

- c) создать пользователя в ручном режиме.

Добавляем строчку в passwd:
```sh
~$ sudo nano /etc/passwd 
#  bogdan:x:1001:1001:Bogdan Pokupaev,,,:/home/bogdan:/bin/bash
```

Добавляем строчку в group:
```sh
~$ sudo nano / tc/group
# bogdan:x:1001:
```
Создаем домашнюю папку пользователя и копируем в нее:
```sh
~$ sudo mkdir /home/bogdan
~$ sudo cp -v /etc/skel/.* /home/bogdan
~$ ll /home/bogdan/
итого 20
drwxr-xr-x 2 root root 4096 окт 18 17:42 ./
drwxr-xr-x 5 root root 4096 окт 18 17:42 ../
-rw-r--r-- 1 root root  220 окт 18 17:42 .bash_logout
-rw-r--r-- 1 root root 3771 окт 18 17:42 .bashrc
-rw-r--r-- 1 root root  807 окт 18 17:42 .profile
```
Дальше надо поменять принадлежность этого каталога и создаем для пользователя пароль:
```sh
~$ sudo chown -Rv bogdan:bogdan /home/bogdan
изменён владелец '/home/bogdan/.bash_logout' с root:root на bogdan:bogdan
изменён владелец '/home/bogdan/.profile' с root:root на bogdan:bogdan
изменён владелец '/home/bogdan/.bashrc' с root:root на bogdan:bogdan
изменён владелец '/home/bogdan' с root:root на bogdan:bogdan
~$ sudo passwd bogdan
Новый пароль : 
Повторите ввод нового пароля : 
passwd: пароль успешно обновлён
```

## 2. Управление группами:
- a) создать группу с использованием утилиты;
```sh
~$ sudo groupadd testing
```

- b) попрактиковаться в смене групп у пользователей;
```sh
~$ sudo usermod -g testing bogdan
~$ id bogdan
uid=1001(bogdan) gid=1002(testing) группы=1002(testing)
```

- c) добавить пользователя в группу, не меняя основной;

```sh
~$ sudo usermod -a -G testing bogdan
~$ groups bogdan
bogdan : bogdan testing
```

- d) удалить пользователя из группы.
```sh
~$ sudo usermod -G bogdan bogdan
~$ groups bogdan
bogdan : bogdan
```

## 3. Суперпользователь
- Создать пользователя с правами суперпользователя:
```sh
~$ sudo usermod -aG sudo bogdan
~$ cat /etc/group | grep sudo
sudo:x:27:zhlznk,bogdan
```
- Сделать так, чтобы sudo не требовал пароль для выполнения команд:

Надо изменить настройки sudo при помощи утилиты visudo

```sh
~$ sudo visudo

#includedir /etc/sudoers.d
bogdan ALL=(ALL:ALL) NOPASSWD: ALL
```






