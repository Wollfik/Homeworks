# Домашнее задание к занятию 12.6. «Репликация и масштабирование. Часть 1»

---

### Задание 1

На лекции рассматривались режимы репликации master-slave, master-master, опишите их различия.

*При репликации Master-Slave, изменеия вносятся в сервер Master, а Slave дублирует данные с Мастера. 
При Мастер-Мстер изменения могут вноситься в оба сервера, и читаться друг с друга, что может вызвать проблему согласованности данных.*

---

### Задание 2
Выполните настройку репликации master-slave, которую можно использовать из лекции.

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
```sql
MariaDB [(none)]> SHOW SLAVE STATUS \G
*************************** 1. row ***************************
                Slave_IO_State: Waiting for master to send event
                   Master_Host: 158.160.39.117
                   Master_User: replication
                   Master_Port: 3306
                 Connect_Retry: 60
               Master_Log_File: mysql-bin.000003
           Read_Master_Log_Pos: 342
                Relay_Log_File: mysql-relay-bin.000002
                 Relay_Log_Pos: 555
         Relay_Master_Log_File: mysql-bin.000003
              Slave_IO_Running: Yes
             Slave_SQL_Running: Yes
               Replicate_Do_DB:
           Replicate_Ignore_DB:
            Replicate_Do_Table:
        Replicate_Ignore_Table:
       Replicate_Wild_Do_Table:
   Replicate_Wild_Ignore_Table:
                    Last_Errno: 0
                    Last_Error:
                  Skip_Counter: 0
           Exec_Master_Log_Pos: 342
               Relay_Log_Space: 864
               Until_Condition: None
                Until_Log_File:
                 Until_Log_Pos: 0
            Master_SSL_Allowed: No
            Master_SSL_CA_File:
            Master_SSL_CA_Path:
               Master_SSL_Cert:
             Master_SSL_Cipher:
                Master_SSL_Key:
         Seconds_Behind_Master: 0
 Master_SSL_Verify_Server_Cert: No
                 Last_IO_Errno: 0
                 Last_IO_Error:
                Last_SQL_Errno: 0
                Last_SQL_Error:
   Replicate_Ignore_Server_Ids:
              Master_Server_Id: 1
                Master_SSL_Crl:
            Master_SSL_Crlpath:
                    Using_Gtid: No
                   Gtid_IO_Pos:
       Replicate_Do_Domain_Ids:
   Replicate_Ignore_Domain_Ids:
                 Parallel_Mode: optimistic
                     SQL_Delay: 0
           SQL_Remaining_Delay: NULL
       Slave_SQL_Running_State: Slave has read all relay log; waiting for more updates
              Slave_DDL_Groups: 0
Slave_Non_Transactional_Groups: 0
    Slave_Transactional_Groups: 0
```
![alt text](https://github.com/Wollfik/Myrepoz/blob/main/Screenshot_2.png)
![alt text](https://github.com/Wollfik/Myrepoz/blob/main/Screenshot_1.png)


---
