# Домашнее задание к занятию "`Работа с данными DDL/DML `" - `Макаров Денис`


### Инструкция по выполнению домашнего задания

   1. Сделайте `fork` данного репозитория к себе в Github и переименуйте его по названию или номеру занятия, например, https://github.com/имя-вашего-репозитория/git-hw или  https://github.com/имя-вашего-репозитория/7-1-ansible-hw).
   2. Выполните клонирование данного репозитория к себе на ПК с помощью команды `git clone`.
   3. Выполните домашнее задание и заполните у себя локально этот файл README.md:
      - впишите вверху название занятия и вашу фамилию и имя
      - в каждом задании добавьте решение в требуемом виде (текст/код/скриншоты/ссылка)
      - для корректного добавления скриншотов воспользуйтесь [инструкцией "Как вставить скриншот в шаблон с решением](https://github.com/netology-code/sys-pattern-homework/blob/main/screen-instruction.md)
      - при оформлении используйте возможности языка разметки md (коротко об этом можно посмотреть в [инструкции  по MarkDown](https://github.com/netology-code/sys-pattern-homework/blob/main/md-instruction.md))
   4. После завершения работы над домашним заданием сделайте коммит (`git commit -m "comment"`) и отправьте его на Github (`git push origin`);
   5. Для проверки домашнего задания преподавателем в личном кабинете прикрепите и отправьте ссылку на решение в виде md-файла в вашем Github.
   6. Любые вопросы по выполнению заданий спрашивайте в чате учебной группы и/или в разделе “Вопросы по заданию” в личном кабинете.
   
Желаем успехов в выполнении домашнего задания!
   
### Дополнительные материалы, которые могут быть полезны для выполнения задания

1. [Руководство по оформлению Markdown файлов](https://gist.github.com/Jekins/2bf2d0638163f1294637#Code)

---
Задание можно выполнить как в любом IDE, так и в командной строке.

### Задание 1 

1.1. Поднимите чистый инстанс MySQL версии 8.0+. Можно использовать локальный сервер или контейнер Docker.


```sh
sudo apt update
sudo apt install gnupg
wget -c https://dev.mysql.com/get/mysql-apt-config_0.8.24-1_all.deb
sudo dpkg -i mysql-apt-config_0.8.24-1_all.deb
sudo apt update
sudo apt install -y mysql-server # задаём пароль 12345 для пользователя root в СУБД MySQL
sudo systemctl status mysql.service
```

1.2. Создайте учётную запись sys_temp.

```sql
mysql -u root -p 
create user 'sys_temp'@'%' identified by 'Root_12root';
exit 
```
1.3. Выполните запрос на получение списка пользователей в базе данных. (скриншот)

```sql
mysql -u root -p 
select User,Host from mysql.user;
exit
```
![Снимок79](https://github.com/Makarov-Denis/12_02-DDL-DML/assets/148921246/2e0dfb7c-e665-471a-9f19-27dfe2a43719)

1.4. Дайте все права для пользователя sys_temp.

```sql
mysql -u root -p 
grant ALL PRIVILEGES on *.* to 'sys_temp'@'%' with GRANT option;
flush privileges;
exit
```

1.5. Выполните запрос на получение списка прав для пользователя sys_temp. (скриншот)

```sql
mysql -u root -p 
show grants for 'sys_temp'@'%';
exit
```

![Снимок80](https://github.com/Makarov-Denis/12_02-DDL-DML/assets/148921246/549d87bc-6895-48d3-8220-4276aca37b17)

1.6. Переподключитесь к базе данных от имени sys_temp.
Для смены типа аутентификации с sha2 используйте запрос:

```sql
ALTER USER 'sys_test'@'localhost' IDENTIFIED WITH mysql_native_password BY 'password';
```
### Запрос представлен ниже:

```sql
mysql -u sys_temp -p 
alter user 'sys_temp'@'%' IDENTIFIED with mysql_native_password by 'Root_12root';
exit
```

1.6. По ссылке https://downloads.mysql.com/docs/sakila-db.zip скачайте дамп базы данных.

```sh
wget -c https://downloads.mysql.com/docs/sakila-db.zip
unzip sakila-db.zip
cd sakila-db
```

1.7. Восстановите дамп в базу данных.

```sql
mysql -u sys_temp -p
show databases;
create database SakilaDB;
show databases;
use SakilaDB;
show tables;
source sakila-schema.sql;
source sakila-data.sql;
show tables;
exit
```

1.8. При работе в IDE сформируйте ER-диаграмму получившейся базы данных. При работе в командной строке используйте команду для получения всех таблиц базы данных. (скриншот)

```sql
mysql -u sys_temp -p
show databases;
use SakilaDB;
show tables;
exit
```

![Снимок81](https://github.com/Makarov-Denis/12_02-DDL-DML/assets/148921246/933a39b7-7888-46a3-bee8-3fb51236a92c)

---

### Задание 2
Составьте таблицу, используя любой текстовый редактор или Excel, в которой должно быть два столбца: в первом должны быть названия таблиц восстановленной базы, во втором названия первичных ключей этих таблиц. Пример: (скриншот/текст)

```
Название таблицы | Название первичного ключа
customer         | customer_id
```

### *Ответ*

```
actor           |   actor_id
address         |   address_id
category        |   category_id
city            |   city_id
country         |   country_id
customer        |   customer_id
film            |   film_id
film_actor      |   actor_id, film_id
film_category   |   film_id, category_id
film_text       |   film_id
inventory       |   inventory_id
language        |   language_id
payment         |   payment_id
rental          |   rental_id
staff           |   staff_id
store           |   store_id
```
---

