# Домашнее задание к занятию «Система мониторинга Zabbix»

В практике есть 2 основных и 1 дополнительное (со звездочкой) задания. Первые два нужно выполнять обязательно, третье - по желанию и его решение никак не повлияет на получение вами зачета по этому домашнему заданию, при этом вы сможете глубже и/или шире разобраться в материале. 

Пожалуйста, присылайте на проверку всю задачу сразу. Любые вопросы по решению задач задавайте в чате учебной группы.

### Цели задания
1. Научиться устанавливать Zabbix Server c веб-интерфейсом
2. Научиться устанавливать Zabbix Agent на хосты
3. Научиться устанавливать Zabbix Agent на компьютер и подключать его к серверу Zabbix 

### Чеклист готовности к домашнему заданию
- [ ] Просмотрите в личном кабинете занятие "Система мониторинга Zabbix" 

### Инструкция по выполнению домашнего задания

1. Сделайте fork [репозитория c шаблоном решения](https://github.com/netology-code/sys-pattern-homework) к себе в Github и переименуйте его по названию или номеру занятия, например, https://github.com/имя-вашего-репозитория/gitlab-hw или https://github.com/имя-вашего-репозитория/8-03-hw).
2. Выполните клонирование этого репозитория к себе на ПК с помощью команды `git clone`.
3. Выполните домашнее задание и заполните у себя локально этот файл README.md:
   - впишите вверху название занятия и ваши фамилию и имя;
   - в каждом задании добавьте решение в требуемом виде: текст/код/скриншоты/ссылка;
   - для корректного добавления скриншотов воспользуйтесь инструкцией [«Как вставить скриншот в шаблон с решением»](https://github.com/netology-code/sys-pattern-homework/blob/main/screen-instruction.md);
   - при оформлении используйте возможности языка разметки md. Коротко об этом можно посмотреть в [инструкции по MarkDown](https://github.com/netology-code/sys-pattern-homework/blob/main/md-instruction.md).
4. После завершения работы над домашним заданием сделайте коммит (`git commit -m "comment"`) и отправьте его на Github (`git push origin`).
5. Для проверки домашнего задания преподавателем в личном кабинете прикрепите и отправьте ссылку на решение в виде md-файла в вашем Github.
6. Любые вопросы задавайте в чате учебной группы и/или в разделе «Вопросы по заданию» в личном кабинете.

---

### Задание 1 

Установите Zabbix Server с веб-интерфейсом.

#### Процесс выполнения
1. Выполняя ДЗ, сверяйтесь с процессом отражённым в записи лекции.
2. Установите PostgreSQL. Для установки достаточна та версия, что есть в системном репозитороии Debian 11.
3. Пользуясь конфигуратором команд с официального сайта, составьте набор команд для установки последней версии Zabbix с поддержкой PostgreSQL и Apache.
4. Выполните все необходимые команды для установки Zabbix Server и Zabbix Web Server.

#### Требования к результаты 
1. Прикрепите в файл README.md скриншот авторизации в админке.
2. Приложите в файл README.md текст использованных команд в GitHub.


#### Решение:
`Статус службы Zabbix Server` - [Zabbix-server](https://github.com/sash3939/Zabbix/assets/156709540/b3a44590-590c-4b24-8c93-b324e7e66fcb)
`Админка Zabbix` - [zabbix Admin](https://github.com/sash3939/Zabbix/assets/156709540/db49dccd-b40c-4231-8ad1-ef4dc3c61007)


`COMMANDS`
#### apt install postgresql ####
#### wget https://repo.zabbix.com/zabbix/6.0/debian/pool/main/z/zabbix-release/zabbix-release_6.0-5+debian12_all.deb ####
#### dpkg -i zabbix-release_6.0-5+debian12_all.deb ####
#### lsof /var/lib/dpkg/lock ####
#### ps cax | grep 945 ####
#### kill 945 ####
#### dpkg -i zabbix-release_6.0-5+debian12_all.deb ####
#### apt update ####
#### apt install zabbix-server-pgsql zabbix-frontend-php php8.2-pgsql zabbix-apache-conf zabbix-sql-scripts ####
#### su - postgres -c 'psql --command "CREATE USER zabbix WITH PASSWORD '\'123456789\'';"' ####
#### sudo -u postgres createdb -O zabbix zabbix ####
#### zcat /usr/share/zabbix-sql-scripts/postgresql/server.sql.gz | sudo -u zabbix psql zabbix ####
#### nano /etc/zabbix/zabbix_server.conf ####
#### zabbix restart zabbix_server apache2 ####
#### systemctl status zabbix-server.service ####
#### systemctl enable zabbix-server.service ####
---

### Задание 2 

Установите Zabbix Agent на два хоста.

#### Процесс выполнения
1. Выполняя ДЗ, сверяйтесь с процессом отражённым в записи лекции.
2. Установите Zabbix Agent на 2 вирт.машины, одной из них может быть ваш Zabbix Server.
3. Добавьте Zabbix Server в список разрешенных серверов ваших Zabbix Agentов.
4. Добавьте Zabbix Agentов в раздел Configuration > Hosts вашего Zabbix Servera.
5. Проверьте, что в разделе Latest Data начали появляться данные с добавленных агентов.

#### Требования к результаты 
1. Приложите в файл README.md скриншот раздела Configuration > Hosts, где видно, что агенты подключены к серверу
2. Приложите в файл README.md скриншот лога zabbix agent, где видно, что он работает с сервером
3. Приложите в файл README.md скриншот раздела Monitoring > Latest data для обоих хостов, где видны поступающие от агентов данные.
4. Приложите в файл README.md текст использованных команд в GitHub

#### Решение
1. Подключены к серверу - [status](https://github.com/sash3939/Zabbix/assets/156709540/f8374bb6-8b84-46be-aca5-481c9ee103c6)
2. Скриншот лога zabbix agent, где видно, что он работает с сервером -[log](https://github.com/sash3939/Zabbix/assets/156709540/b3f73406-98cd-46e8-9cc5-9e8b6d777cee)
3. Скриншот раздела Monitoring > Latest data для обоих хостов, где видны поступающие от агентов данные. -
`[Agent1](https://github.com/sash3939/Zabbix/assets/156709540/a541f3bb-5bc7-4b83-b74a-0680c12ebb58), [Memory_Graph_Agent1](https://github.com/sash3939/Zabbix/assets/156709540/1e704acd-040e-4e5c-96e6-9a5675f27175)`
`[Agent2](https://github.com/sash3939/Zabbix/assets/156709540/4afbc5de-19f0-4500-a279-3735ed6362dc), [Memory_Grapg_Agent2](https://github.com/sash3939/Zabbix/assets/156709540/e75b0166-41ab-4b4e-b122-a32ba3f3e8db)`
5. Приложите в файл README.md текст использованных команд в GitHub -
### tail -f /var/log/zabbix/zabbix_agent.log

---
## Задание 3 со звёздочкой*
Установите Zabbix Agent на Windows (компьютер) и подключите его к серверу Zabbix.

#### Требования к результаты. Решение:
1. Скриншот раздела Latest Data, где видно свободное место на диске C: - [free space](https://github.com/sash3939/Zabbix/assets/156709540/fca2ccf5-d082-4607-b5ef-b19681ab79e3)

--- 

## Критерии оценки

1. Выполнено минимум 2 обязательных задания
2. Прикреплены требуемые скриншоты и тексты 
3. Задание оформлено в шаблоне с решением и опубликовано на GitHub
