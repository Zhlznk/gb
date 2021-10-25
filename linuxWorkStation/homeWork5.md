# 1. 

- Создать файл file1 и наполнить его произвольным содержимым.
```sh
~/2gb/test$ echo "Набрать произвольный текст" > file1
```
- Скопировать его в file2.
```sh
~/2gb/test$ cp file1 file2
```
- Создать символическую ссылку file3 на file1.
```sh
~/2gb/test$ ln -s file1 file3
~/2gb/test$ ll f*
-rw-rw-r-- 1 zhlznk zhlznk 51 окт 25 17:06 file1
-rw-rw-r-- 1 zhlznk zhlznk 51 окт 25 17:08 file2
lrwxrwxrwx 1 zhlznk zhlznk  5 окт 25 17:16 file3 -> file1
```

- Создать жёсткую ссылку file4 на file1. Посмотреть, какие inode у файлов.
```sh
~/2gb/test$ ln file1 file4
~/2gb/test$ ll -i f*
1047106 -rw-rw-r-- 2 zhlznk zhlznk 51 окт 25 17:06 file1
1047130 -rw-rw-r-- 1 zhlznk zhlznk 51 окт 25 17:08 file2
1048407 lrwxrwxrwx 1 zhlznk zhlznk  5 окт 25 17:16 file3 -> file1
1047106 -rw-rw-r-- 2 zhlznk zhlznk 51 окт 25 17:06 file4
```

- Удалить file1.
```sh
~/2gb/test$ rm file1

```
- Попробовать вывести их на экран остальные файлы.
```sh
~/2gb/test$ cat file2
Набрать произвольный текст
~/2gb/test$ cat file3
cat: file3: Нет такого файла или каталога
~/2gb/test$ cat file4
Набрать произвольный текст
```

- Что стало с остальными созданными файлами?

Скопированный файл file2 остался неизменным.
Символическая ссылка file3 не открывается. Появлется общение, что такого файла или каталога нет.
Файл жёсткой ссылки открывается, содержимое осталось на месте.

# 2. 

- Дать созданным файлам другие, произвольные имена. 
```sh
~/2gb/test$ mv file2 file_copy
~/2gb/test$ mv file4 file_hl
~/2gb/test$ ln -s file_copy copy_sl
```

- Создать новые символические ссылки.
```sh
~/2gb/test$ ln -s file_copy copy_sl 
~/2gb/test$ cat copy_sl 
Набрать произвольный текст
~/2gb/test$ ln -s file_hl hard_sl 
~/2gb/test$ cat hard_sl 
Набрать произвольный текст
```

- Переместить ссылки в другую директорию.
```sh
~/2gb/test$ mkdir subtest
~/2gb/test$ mv copy_sl subtest/copy_sl
zhlznk@zhlznk-X75VB:~/2gb/test$ cat subtest/copy_sl 
cat: subtest/copy_sl: Нет такого файла или каталога
```
При открытии жёсткой ссылки выдается ошибка.

```sh
~/2gb/test$ mv hard_sl subtest/hard_sl
~/2gb/test$ cat subtest/hard_sl 

```
То же самое.

# 3. 

- Создать два произвольных файла.
```sh
~/2gb/test$ touch mag mega
```

- Первому присвоить права на чтение и запись для владельца и группы, только на чтение — для всех. Сделать это в численном и символьном виде.
```sh
~/2gb/test$ ls -l mag
-rw-rw-r-- 1 zhlznk zhlznk 0 окт 25 18:20 mag
```
или
```sh
~/2gb/test$ chmod ugo=rw mag
~/2gb/test$ ls -l mag
-rw-rw-rw- 1 zhlznk zhlznk 0 окт 25 18:20 mag
```
- Второму присвоить права на чтение и запись только для владельца. Сделать это в численном и символьном виде.
```sh
~/2gb/test$ chmod 600 mega
~/2gb/test$ ls -l mega 
-rw------- 1 zhlznk zhlznk 0 окт 25 18:20 mega
```
