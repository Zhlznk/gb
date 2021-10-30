# 1. 
- Подключить репозиторий с nginx любым удобным способом, установить nginx и потом удалить nginx, используя утилиту dpkg.

[Инструкция] по установке.
Подготовка к установке:
```sh
~$ sudo apt install curl gnupg2 ca-certificates lsb-release ubuntu-archive-keyring
~$ curl https://nginx.org/keys/nginx_signing.key | gpg --dearmor | sudo tee /usr/share/keyrings/nginx-archive-keyring.gpg >/dev/null
~$ gpg --dry-run --quiet --import --import-options import-show /usr/share/keyrings/nginx-archive-keyring.gpg
~$ echo "deb [signed-by=/usr/share/keyrings/nginx-archive-keyring.gpg] \ http://nginx.org/packages/ubuntu `lsb_release -cs` nginx" | sudo tee /etc/apt/sources.list.d/nginx.list
~$ echo -e "Package: *\nPin: origin nginx.org\nPin: release o=nginx\nPin-Priority: 900\n" | sudo tee /etc/apt preferences.d/99nginx
```
Установка и проверка:
```sh
~$ sudo apt update
~$ sudo apt install nginx
~$ sudo service nginx start
~$ sudo service nginx status
● nginx.service - nginx - high performance web server
     Loaded: loaded (/lib/systemd/system/nginx.service; enabled; vendor preset: enabled)
     Active: active (running) since Sat 2021-10-30 11:09:28 MSK; 3h 23min ago
       Docs: https://nginx.org/en/docs/
    Process: 4546 ExecStart=/usr/sbin/nginx -c /etc/nginx/nginx.conf (code=exited, status=0/SUCCESS)
   Main PID: 4547 (nginx)
      Tasks: 2 (limit: 5474)
     Memory: 1.7M
     CGroup: /system.slice/nginx.service
             ├─4547 nginx: master process /usr/sbin/nginx -c /etc/nginx/nginx.conf
             └─4548 nginx: worker process

окт 30 11:09:28 virta-VirtualBox systemd[1]: Starting nginx - high performance web server...
окт 30 11:09:28 virta-VirtualBox systemd[1]: nginx.service: Can't open PID file /run/nginx.pid (yet?) after start: Operation not permitted
окт 30 11:09:28 virta-VirtualBox systemd[1]: Started nginx - high performance web server.
```
Удаление:
```sh
~$ sudo dpkg --remove nginx
(Чтение базы данных … на данный момент установлено 188408 файлов и каталогов.)
Удаляется nginx (1.20.1-1~focal) …
Обрабатываются триггеры для man-db (2.9.1-1) …
```

# 2. 
- Установить пакет на свой выбор, используя snap.
```sh
~$ sudo snap install curl  # version 7.79.1
```

# 3. 
- Настроить iptables: разрешить подключения только на 22-й и 80-й порты.
```sh
~$ sudo iptables -t filter -A INPUT -p tcp --dport 80 -j ACCEPT
~$ sudo iptables -t filter -A INPUT -p tcp --dport 22 -j ACCEPT
~$ sudo iptables -P INPUT DROP
```

[Иструкция]: <https://nginx.org/ru/linux_packages.html>
