# otus-zbx
Demo for otus webinar

# Запуск стенда

Требуется Vagrant и Virtualbox.

## Подготовка виртуальных машин

```
vagrant up
```

Будут сконфигурированы 3 виртуальные машины: zabbix, web, ansible

* Zabbix: zabbix-сервер
* Web: web-сервер для демонстрации подключения к мониторингу
* Ansible: ansible для установки софта на 2 предыдущих

## Правим hosts

В /etc/hosts добавляем строки:

```
192.168.50.11   zabbix.otus.example
192.168.50.12	wp.otus.example
```

# Вход в веб-интерфейс Zabbix:

http://zabbix.otus.example

```
Login: Admin
Password: zabbix
```
