## Задача 1

Вывести отсортированный в алфавитном порядке список имен пользователей в файле passwd (вам понадобится grep).

**Решение:**

```bash
cat /etc/passwd | grep -oE "^[^:]*" | sort
```

![image](https://github.com/user-attachments/assets/f3b8414d-2a9f-419a-a404-076426398e56)

## Задача 2

Вывести данные /etc/protocols в отформатированном и отсортированном порядке для 5 наибольших портов, как показано в примере ниже:

```
[root@localhost etc]# cat /etc/protocols ...
142 rohc
141 wesp
140 shim6
139 hip
138 manet
```

**Решение:**

```bash
cat etc/protocols | sort -k2,2 -r -n | head -n 5 | awk '{print $2, $1}'
```

![image](https://github.com/user-attachments/assets/722552ed-33d9-402e-9395-5f9a947d98c6)

## Задача 3

Написать программу banner средствами bash для вывода текстов, как в следующем примере (размер баннера должен меняться!):

```
[root@localhost ~]# ./banner "Hello from RTU MIREA!"
+-----------------------+
| Hello from RTU MIREA! |
+-----------------------+
```

**Решение:**

```py
#! /bin/python3

import sys
s = sys.argv[1]

line = f'+{"-" * (len(s) + 2)}+'

print(line)
print(f'| {s} |')
print(line)
```

![image](https://github.com/user-attachments/assets/1e260f9a-9822-4d5b-9a9d-675b7632fbd1)

![image](https://github.com/user-attachments/assets/b9ee1221-9768-4708-9f6c-f9b49dbe63a4)

## Задача 4

Написать программу для вывода всех идентификаторов (по правилам C/C++ или Java) в файле (без повторений).

Пример для hello.c:

```
h hello include int main n printf return stdio void world
```

**Решение:**

```bash
cat hello.c | grep -Eo "\b[a-zA-Z_][0-9a-zA-Z_]*\b" | sort -u
```

![Снимок экрана от 2024-09-07 09-41-23](https://github.com/user-attachments/assets/a11132e8-886c-4f01-8527-8b47f0acd31e)

## Задача 5

Написать программу для регистрации пользовательской команды (правильные права доступа и копирование в /usr/local/bin).

Например, пусть программа называется reg:

```
./reg banner
```

**Решение:**

```bash
#! /usr/bin/bash

chmod ugo+x $1
sudo cp $1 /usr/local/bin
```

![image](https://github.com/user-attachments/assets/dda243ac-a460-488e-90b9-ef4b50a44586)

## Задача 6

Написать программу для проверки наличия комментария в первой строке файлов с расширением c, js и py.

**Решение:**

```py
#! /usr/bin/python3
from sys import argv, exit

f_name = argv[1]
f = open(f_name, 'rt')
line = f.readline().strip()
is_comment = False
if f_name.endswith(' .py'):
    if line.startswith(('#', '"""', "'''")):
        is_comment = True
elif f_name.endswith(('.c', '.js')):
    if line.startswith(('//', '/*')):
        is_comment = True
else:
    print('wrong file extension')
    exit()

if is_comment:
    print('comment present')
else:
    print('no comments')

```

![image](https://github.com/user-attachments/assets/c2a21208-9a62-45bc-a28f-1b4ee33ef61d)

## Задача 7

Написать программу для нахождения файлов-дубликатов (имеющих 1 или более копий содержимого) по заданному пути (и подкаталогам).

**Решение:**

```bash
find "$1" -type f -exec md5sum {} + | sort | uniq -w32 -dD
```

![image](https://github.com/user-attachments/assets/7ffe9708-32c1-473f-a99e-635e0e4a1499)


## Задача 8

Написать программу, которая находит все файлы в данном каталоге с расширением, указанным в качестве аргумента и архивирует все эти файлы в архив tar.

**Решение:**

```bash
find . -name "*.$1" -print0 | tar -czf archive.tar.gz --null -T -
```

![image](https://github.com/user-attachments/assets/c326b7c2-3269-40d0-a33f-2d0e2944f633)


## Задача 9

Написать программу, которая заменяет в файле последовательности из 4 пробелов на символ табуляции. Входной и выходной файлы задаются аргументами.

**Решение:**

```bash
sed -i 's/    /\t/g' "$1"
```

![image](https://github.com/user-attachments/assets/95aa9477-9712-4301-84f8-7903f519bf81)


## Задача 10

Написать программу, которая выводит названия всех пустых текстовых файлов в указанной директории. Директория передается в программу параметром. 

**Решение:**

```bash
find "$1" -type f -empty -name "*.txt"
```


![image](https://github.com/user-attachments/assets/2a70ef25-93b4-4ef5-ac51-b2630b4f152a)

