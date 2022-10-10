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

## Запускаем установку софта ансиблом

### Установка зависимостей

```
vagrant ssh ansible

ansible-galaxy collection install -r /otus/requirements.yml
ansible-galaxy role install -r /otus/requirements.yml
```

### Установка софта на виртуальные машины

```
ansible-playbook -i /otus/otus.inv /otus/zabbix.yml
ansible-playbook -i /otus/otus.inv /otus/wordpress-lamp_ubuntu1804/playbook.yml
```

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
