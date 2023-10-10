# Домашнее задание к занятию "Система монитринга Zabbix - часть 1"
# Козлов Станислав

## Задание 1
### Установка Zabbix Server

```
wget https://repo.zabbix.com/zabbix/6.0/debian/pool/main/z/zabbix-release/zabbix-release_6.0-4+debian11_all.deb
dpkg -i zabbix-release_6.0-4+debian11_all.deb
apt update

apt install zabbix-server-pgsql zabbix-frontend-php php7.4-pgsql zabbix-apache-conf zabbix-sql-scripts zabbix-agent
```
### Установка и настройка PostgreSQL

```
sudo apt install postgresql postgresql-contrib
sudo -u postgres createuser --pwprompt zabbix
sudo -u postgres createdb -O zabbix zabbix
```
### Импорт начальной схемы и данных

`zcat /usr/share/zabbix-sql-scripts/postgresql/server.sql.gz | sudo -u zabbix psql zabbix`

В файле `/etc/zabbix/zabbix_server.conf` резактируем строку DBPassword

Переходим по адресу http://127.0.0.1/zabbix и завершаем установку

![Админка Zabbix](https://github.com/stkv1/zabbix-01/blob/main/img/002.PNG)

## Задание 2

### Установка Zabbix Agent

```
wget https://repo.zabbix.com/zabbix/6.0/debian/pool/main/z/zabbix-release/zabbix-release_6.0-4+debian11_all.deb
dpkg -i zabbix-release_6.0-4+debian11_all.deb 
apt update
apt install zabbix-agent
systemctl restart zabbix-agent
systemctl enable zabbix-agent
```
![Запущенный Zabbix Agent](https://github.com/stkv1/zabbix-01/blob/main/img/003.PNG)

Разрешаем подключения сервера к агенту в `/etc/zabbix/zabbix_agentd.conf`

![лог Zabbix-агента](https://github.com/stkv1/zabbix-01/blob/main/img/012.PNG)

![Активные агенты в панели управления](https://github.com/stkv1/zabbix-01/blob/main/img/006.PNG)

![Данные от агентов](https://github.com/stkv1/zabbix-01/blob/main/img/013.PNG)

## Задание 3

Активные агенты в панели управления:

![Активные агенты в панели управления](https://github.com/stkv1/zabbix-01/blob/main/img/009.PNG)

Использование диска C:

![Использование диска C:](https://github.com/stkv1/zabbix-01/blob/main/img/010.PNG)