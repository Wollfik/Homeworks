# Домашнее задание к занятию 12.6. «Репликация и масштабирование. Часть 1»

---

### Задание 1

На лекции рассматривались режимы репликации master-slave, master-master, опишите их различия.

*При репликации Master-Slave, изменеия вносятся в сервер Master, а Slave дублирует данные с Мастера. 
При Мастер-Мстер изменения могут вноситься в оба сервера, и читаться друг с друга, что может вызвать проблему согласованности данных.*

---

### Задание 2
На Мастер
```conf
[mysqld]
pid-file             = /run/mysqld/mysqld.pid
basedir              = /usr
bind-address         = 0.0.0.0
server-id            = 1
log_bin              = /var/log/mysql/mysql-bin.log
log_bin_index        = /var/log/mysql/mysql-bin.log.index
relay_log            = /var/log/mysql/mysql-relay-bin
relay_log_index      = /var/log/mysql/mysql-relay-bin.index
expire_logs_days     = 10
character-set-server = utf8mb4
collation-server     = utf8mb4_general_ci
```

```sql
MariaDB [(none)]> SHOW SLAVE STATUS \G;
Empty set (0.000 sec)
```

На Slave
```
[mysqld]
pid-file              = /run/mysqld/mysqld.pid
basedir               = /usr
bind-address          = 0.0.0.0
server-id             = 2
log_bin               = /var/log/mysql/mysql-bin.log
log_bin_index         = /var/log/mysql/mysql-bin.log.index
relay_log             = /var/log/mysql/mysql-relay-bin
relay_log_index       = /var/log/mysql/mysql-relay-bin.index
expire_logs_days      = 10
character-set-server  = utf8mb4
collation-server      = utf8mb4_general_ci
```
Выполните настройку репликации master-slave, которую можно использовать из лекции.
![alt text](https://github.com/Wollfik/Myrepoz/blob/main/Screenshot_2.png)
![alt text](https://github.com/Wollfik/Myrepoz/blob/main/Screenshot_1.png)


---

## Дополнительные задания (со звёздочкой*)
Эти задания являются дополнительными, то есть не являются обязательными к выполнению, и никак не повлияют на получение от нас зачёта по домашнему заданию. Вы можете их контролировать, если глубже разобраться в материале.

---

### Задание 3*

Выполните настройку master-master репликации. Произведем проверку.

*Прилагаем эскизный план, выполнение работы: состояние и режимы работы серверов.*
