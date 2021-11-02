# 1. Переустановить операционную систему, подключить репозиторий Docker.

- Переустановить операционную систему:

- Подключить репозиторий Docker:

[Инструкция] по установке. 

Подготовка к установке:
```sh
 ~$ sudo apt-get remove docker docker-engine docker.io containerd runc
 ~$ sudo apt-get update
 ~$  sudo apt-get install \
    ca-certificates \
    curl \
    gnupg \
    lsb-release
 ~$ curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg
 ~$ echo   "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://download.docker.com/linux/ubuntu \
 ```

 Установка:
 ```sh
 ~$ sudo apt-get update
 ~$ sudo apt-get install docker-ce docker-ce-cli containerd.io
 ```


# 2. Запустить контейнер с Ubuntu.

```sh
~$ apt-cache madison docker-ce
xxxxxx xxxxxxxxxxxxxxxx
 docker-ce | 5:19.03.12~3-0~ubuntu-focal | https://download.docker.com/linux/ubuntu focal/stable amd64 Packages
 docker-ce | 5:19.03.11~3-0~ubuntu-focal | https://download.docker.com/linux/ubuntu focal/stable amd64 Packages
 docker-ce | 5:19.03.10~3-0~ubuntu-focal | https://download.docker.com/linux/ubuntu focal/stable amd64 Packages
~$ sudo apt-get install docker-ce=5:19.03.9~3-0~ubuntu-focal docker-ce-cli=5:19.03.9~3-0~ubuntu-focal containerd.io
~$ docker run -it ubuntu bash
root@1f9929c2b6c9:/# cat /etc/lsb-release
DISTRIB_ID=Ubuntu
DISTRIB_RELEASE=20.04
DISTRIB_CODENAME=focal
DISTRIB_DESCRIPTION="Ubuntu 20.04.3 LTS"
root@1f9929c2b6c9:/# exit
exit
```

[Инструкция]: <https://docs.docker.com/engine/install/ubuntu/>