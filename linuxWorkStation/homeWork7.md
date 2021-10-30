# 1. 
- Подключить репозиторий с nginx любым удобным способом, установить nginx и потом удалить nginx, используя утилиту dpkg.

[Инструкция] по установке.
Подготовка к установке:
```sh
~$ sudo apt install curl gnupg2 ca-certificates lsb-release ubuntu-archive-keyring
~$ curl https://nginx.org/keys/nginx_signing.key | gpg --dearmor | sudo tee /usr/share/keyrings/nginx-archive-keyring.gpg >/dev/null
~$ gpg --dry-run --quiet --import --import-options import-show /usr/share/keyrings/nginx-archive-keyring.gpg
~$ echo "deb [signed-by=/usr/share/keyrings/nginx-archive-keyring.gpg] \ http://nginx.org/packages/ubuntu `lsb_release -cs` nginx" | sudo tee /etc/apt/sources.list.d/nginx.list
~$ echo -e "Package: *\nPin: origin nginx.org\nPin: release o=nginx\nPin-Priority: 900\n" \
    | sudo tee /etc/apt/preferences.d/99nginx
```
Установка и проверка:
```sh
~$ sudo apt update
~$ sudo apt install nginx
~$ sudo service nginx start
~$ sudo service nginx status 
[sudo] пароль для zhlznk: 
● nginx.service - nginx - high performance web server
     Loaded: loaded (/lib/systemd/system/nginx.service; enabled; vendor preset:>
     Active: active (running) since Sat 2021-10-30 21:35:19 MSK; 4h 0min ago
       Docs: https://nginx.org/en/docs/
    Process: 14494 ExecStart=/usr/sbin/nginx -c /etc/nginx/nginx.conf (code=exi>
   Main PID: 14495 (nginx)
      Tasks: 5 (limit: 9344)
     Memory: 4.9M
     CGroup: /system.slice/nginx.service
             ├─14495 nginx: master process /usr/sbin/nginx -c /etc/nginx/nginx.>
             ├─14496 nginx: worker process
             ├─14497 nginx: worker process
             ├─14498 nginx: worker process
             └─14499 nginx: worker process

окт 30 21:35:19 zhlznk-X75VB systemd[1]: Starting nginx - high performance web >
окт 30 21:35:19 zhlznk-X75VB systemd[1]: Started nginx - high performance web s>
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
~$ sudo iptables -L
[sudo] пароль для virta: 
Chain INPUT (policy DROP)
target     prot opt source               destination         
ACCEPT     tcp  --  anywhere             anywhere             tcp dpt:http
ACCEPT     tcp  --  anywhere             anywhere             tcp dpt:ssh

Chain FORWARD (policy ACCEPT)
target     prot opt source               destination         

Chain OUTPUT (policy ACCEPT)
target     prot opt source               destination   
```

[Иструкция]: <https://nginx.org/ru/linux_packages.html>
