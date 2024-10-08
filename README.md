## Домашнее задание к занятию «Работа с данными (DDL/DML)» -Рустам Ахмадеев
## Инструкция по выполнению домашнего задания
1. Сделайте fork репозитория c шаблоном решения к себе в Github и переименуйте его по названию или номеру занятия, например, https://github.com/имя-вашего-репозитория/gitlab-hw или https://github.com/имя-вашего-репозитория/8-03-hw).
2. Выполните клонирование этого репозитория к себе на ПК с помощью команды git clone.
3. Выполните домашнее задание и заполните у себя локально этот файл README.md:
- впишите вверху название занятия и ваши фамилию и имя;
- в каждом задании добавьте решение в требуемом виде: текст/код/скриншоты/ссылка;
- для корректного добавления скриншотов воспользуйтесь инструкцией «Как вставить скриншот в шаблон с решением»;
- при оформлении используйте возможности языка разметки md. Коротко об этом можно посмотреть в инструкции по MarkDown.
4. После завершения работы над домашним заданием сделайте коммит (git commit -m "comment") и отправьте его на Github (git push origin).
5. Для проверки домашнего задания преподавателем в личном кабинете прикрепите и отправьте ссылку на решение в виде md-файла в вашем Github.
6. Любые вопросы задавайте в чате учебной группы и/или в разделе «Вопросы по заданию» в личном кабинете.
Желаем успехов в выполнении домашнего задания.

Задание можно выполнить как в любом IDE, так и в командной строке.

## Задание 1
1.1. Поднимите чистый инстанс MySQL версии 8.0+. Можно использовать локальный сервер или контейнер Docker.

1.2. Создайте учётную запись sys_temp.

1.3. Выполните запрос на получение списка пользователей в базе данных. (скриншот)

1.4. Дайте все права для пользователя sys_temp.

1.5. Выполните запрос на получение списка прав для пользователя sys_temp. (скриншот)

1.6. Переподключитесь к базе данных от имени sys_temp.

Для смены типа аутентификации с sha2 используйте запрос:

ALTER USER 'sys_test'@'localhost' IDENTIFIED WITH mysql_native_password BY 'password';
1.6. По ссылке https://downloads.mysql.com/docs/sakila-db.zip скачайте дамп базы данных.

1.7. Восстановите дамп в базу данных.

1.8. При работе в IDE сформируйте ER-диаграмму получившейся базы данных. При работе в командной строке используйте команду для получения всех таблиц базы данных. (скриншот)

Результатом работы должны быть скриншоты обозначенных заданий, а также простыня со всеми запросами.

Решение 1

Установлена mysql

```
sudo apt update && sudo apt upgrade -y
sudo apt install mysql-server
sudo service mysql status
```
![alt text](https://github.com/ahmrust/Working-with-data-DDL-DML-/blob/main/img/9.png)

Создание учетной записи sys_temp
```
mysql -u root -p
CREATE USER 'sys_temp'@'localhost' identified by 'password';
```
![alt text](https://github.com/ahmrust/Working-with-data-DDL-DML-/blob/main/img/7.png)

Запрос получения списка пользователей
```
select user from mysql.user;
```
![alt text](https://github.com/ahmrust/Working-with-data-DDL-DML-/blob/main/img/1.png)

Наделение привелегиями sys_temp
```
grant all privileges on *.* to 'sys_temp'@'localhost' with grant option;
flush privileges;
```
![alt text](https://github.com/ahmrust/Working-with-data-DDL-DML-/blob/main/img/2.png)

Запрос на получение списка прав пользователя sys_temp
```
SHOW GRANTS FOR 'sys_temp'@'localhost';
exit
```
![alt text](https://github.com/ahmrust/Working-with-data-DDL-DML-/blob/main/img/7.png)

Переподключение к базе от имени sys_temp
```
mysql -u sys_temp -p
exit
```
![alt text](https://github.com/ahmrust/Working-with-data-DDL-DML-/blob/main/img/3.png)

Смена типа аутенфикаци
```
mysql -u root -p
ALTER USER 'sys_test'@'localhost' IDENTIFIED WITH mysql_native_password BY 'password';
exit
```
![alt text](https://github.com/ahmrust/Working-with-data-DDL-DML-/blob/main/img/4.png)

Скачан и восстановлен дамп в базу данных
```
wget https://downloads.mysql.com/docs/sakila-db.zip

unzip sakila-db.zip
mysql -p -h 127.0.0.1 -P 3306 -u sys_temp -p < sakila-db/sakila-schema.sql
mysql -p -h 127.0.0.1 -P 3306 -u sys_temp -p < sakila-db/sakila-data.sql
```
![alt text](https://github.com/ahmrust/Working-with-data-DDL-DML-/blob/main/img/5.png)

Сформирована ER-диаграмма получившейся базы данных, получены все таблицы базы данных
```
mysql -u sys_temp -p
show databases;
use sakila;
show tables;
```
Для подключения к базе данных через dbeaver
```
sudo nano /etc/mysql/mysql.conf.d/mysqld.cnf
bind-address            = 0.0.0.0
sudo systemctl restart mysql.service
```
![alt text](https://github.com/ahmrust/Working-with-data-DDL-DML-/blob/main/img/6.png)

## Задание 2
Составьте таблицу, используя любой текстовый редактор или Excel, в которой должно быть два столбца: в первом должны быть названия таблиц восстановленной базы, во втором 
названия первичных ключей этих таблиц. Пример: (скриншот/текст)

Название таблицы | Название первичного ключа
customer         | customer_id

Решение 2

```
Название таблицы             | Название первичного ключа
actor                        | actor_id
actor_info                   |
address                      | address_id
category                     | category_id
city                         | city_id
country                      | country_id
customer                     | customer_id
customer_list                |
film                         | film_id
film_actor                   | actor_id
film_category                | film_id   category_id
staff_list                   |
film_text                    | film_id
inventory                    | inventory_id
language                     | language_id
nicer_but_slower_film_list   |
payment                      | payment_id
rental                       | rental_id
sales_by_film_category       |
sales_by_store               |
staff                        | staff_id
film_list                    |
store                        | store_id

```

## Дополнительные задания (со звёздочкой*)
Эти задания дополнительные, то есть не обязательные к выполнению, и никак не повлияют на получение вами зачёта по этому домашнему заданию. Вы можете их выполнить, если хотите глубже шире разобраться в материале.

## Задание 3*
3.1. Уберите у пользователя sys_temp права на внесение, изменение и удаление данных из базы sakila.

3.2. Выполните запрос на получение списка прав для пользователя sys_temp. (скриншот)

Результатом работы должны быть скриншоты обозначенных заданий, а также простыня со всеми запросами.

