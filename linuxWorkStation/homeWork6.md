# 1. 
- Написать скрипт, который удаляет из текстового файла пустые строки и заменяет маленькие символы на большие. Воспользуйтесь tr или SED.

```sh
$ cat mag
1. Написать скрипт

2. Создать однострочный скрипт

3. * Использовать команду AWK

4. Используя grep, проанализировать файл /var/log/syslog, отобрав события на своё усмотрение.




Сдайте задание до: 27 окт., 19:00 MSK
```
A few moments later:

```sh
$ cat mag | sed 's/[[:alpha:]]/\U&/g; /^$/d'
1. НАПИСАТЬ СКРИПТ
2. СОЗДАТЬ ОДНОСТРОЧНЫЙ СКРИПТ
3. * ИСПОЛЬЗОВАТЬ КОМАНДУ AWK
4. ИСПОЛЬЗУЯ GREP, ПРОАНАЛИЗИРОВАТЬ ФАЙЛ /VAR/LOG/SYSLOG, ОТОБРАВ СОБЫТИЯ НА СВОЁ УСМОТРЕНИЕ.
СДАЙТЕ ЗАДАНИЕ ДО: 27 ОКТ., 19:00 MSK
```
# 2.
- Создать однострочный скрипт, который создаст директории для нескольких годов (2010–2017), в них — поддиректории для месяцев (от 01 до 12), и в каждый из них запишет несколько файлов с произвольными записями. Например, 001.txt, содержащий текст «Файл 001», 002.txt с текстом «Файл 002» и т. д.

```sh
for ((year=2010; year<=2017; year+=1)); 
    do 
        for month in {01..12}; 
            do 
                way=calendar/$year/$month/;
                mkdir -p $way;
                count=$((1 + RANDOM % 3));
                for ((name=1; name<=$count; name+=1)); 
                    do
                        echo "Файл 00$name" > $way/00$name.txt;
                done;     
        done;
done;
```
В строчку будет выглядеть:
 ```sh
 $ for ((year=2010; year<=2017; year+=1)); do for month in {01..12}; do way=calendar/$year/$month/; mkdir -p $way; count=$((1 + RANDOM % 3)); for ((name=1; name<=$count; name+=1)); do echo "Файл 00$name" > $way/00$name.txt; done; done; done;

 ```
 Результат:
 ```sh
 $ tree calendar/
calendar/
├── 2010
│   ├── 01
│   │   ├── 001.txt
│   │   └── 002.txt
│   ├── 02
│   │   ├── 001.txt
│   │   ├── 002.txt
│   │   └── 003.txt
```
```sh
$ cat calendar/2017/12/003.txt 
Файл 003
```


# 4.
- Используя grep, проанализировать файл /var/log/syslog, отобрав события на своё усмотрение.

Меня интересовало, что происходило, Oct 27 17:17:44, с участием avahi-daemon, в строке, где есть символы DNS:

```sh
$ cat /var/log/syslog | grep -iE "DNS" | grep -iE "avahi-daemon" | grep -iE "Oct 27 17:17:44"
Oct 27 17:17:44 zhlznk-xx avahi-daemon[760]: New relevant interface wlp3s0f0.IPv6 for mDNS.
Oct 27 17:17:44 zhlznk-xx avahi-daemon[760]: Joining mDNS multicast group on interface wlp3s0f0.IPv4 with address xxx.xxx.x.xx.
Oct 27 17:17:44 zhlznk-xx avahi-daemon[760]: New relevant interface wlp3s0f0.IPv4 for mDNS.
```


# 5.
- Создать разовое задание на перезагрузку операционной системы, используя at.

```sh
~$ at now + 1 minutes
warning: commands will be executed using /bin/sh
at> shutdown -r now
at> <EOT>
job 7 at Wed Oct 27 17:28:00 2021
```