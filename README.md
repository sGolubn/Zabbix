# Домашнее задание к занятию "`Система мониторинга Zabbix`" - `Голуб Сергей`


### Инструкция по выполнению домашнего задания

   1. Сделайте `fork` данного репозитория к себе в Github и переименуйте его по названию или номеру занятия, например, https://github.com/имя-вашего-репозитория/git-hw или  https://github.com/имя-вашего-репозитория/7-1-ansible-hw).
   2. Выполните клонирование данного репозитория к себе на ПК с помощью команды `git clone`.
   3. Выполните домашнее задание и заполните у себя локально этот файл README.md:
      - впишите вверху название занятия и вашу фамилию и имя
      - в каждом задании добавьте решение в требуемом виде (текст/код/скриншоты/ссылка)
      - для корректного добавления скриншотов воспользуйтесь [инструкцией "Как вставить скриншот в шаблон с решением](https://github.com/netology-code/sys-pattern-homework/blob/main/screen-instruction.md)
      - при оформлении используйте возможности языка разметки md (коротко об этом можно посмотреть в [инструкции  по MarkDown](https://github.com/netology-code/sys-pattern-homework/blob/main/md-instruction.md))
   4. После завершения работы над домашним заданием сделайте коммит (`git commit -m "comment"`) и отправьте его на Github (`git push origin`);
   5. В личном кабинете прикрепите и отправьте ссылку на решение в виде md-файла в вашем Github.
   6. Любые вопросы по выполнению заданий спрашивайте в разделе “Вопросы по заданию” в личном кабинете.
   
Желаем успехов в выполнении домашнего задания!
   
### Дополнительные материалы, которые могут быть полезны для выполнения задания

1. [Руководство по оформлению Markdown файлов](https://gist.github.com/Jekins/2bf2d0638163f1294637#Code)

---

### Задание 1
### Установите Zabbix Server с веб-интерфейсом.

`Процесс выполнения`

1. `Выполняя ДЗ, сверяйтесь с процессом отражённым в записи лекции.`
2. `Установите PostgreSQL. Для установки достаточна та версия, что есть в системном репозитороии Debian 11.`
3. `Пользуясь конфигуратором команд с официального сайта, составьте набор команд для установки последней версии Zabbix с поддержкой PostgreSQL и Apache`
4. `Выполните все необходимые команды для установки Zabbix Server и Zabbix Web Server`
`Требования к результатам`
1. `Прикрепите в файл README.md скриншот авторизации в админке.`
2. `Приложите в файл README.md текст использованных команд в GitHub.`

### Решение 1 

1. `sudo apt update`
2. `sudo apt install postgersql`
3. `sudo wget https://repo.zabbix.com/zabbix/6.0/ubuntu/pool/main/z/zabbix-release/zabbix-release_latest_6.0+ubuntu24.04_all.deb`
4. `sudo dpkg -i zabbix-release_latest_6.0+ubuntu24.04_all.deb`
5. `sudo apt update`
6. `sudo apt install zabbix-server-pgsql zabbix-frontend-php php8.3-pgsql zabbix-apache-conf zabbix-sql-scripts`
7. `sudo -u postgres createuser --pwprompt zabbix`
8. `sudo -u postgres createdb -O zabbix zabbix zcat /usr/share/zabbix-sql-scripts/postgresql/server.sql.gz | sudo -u zabbix psql zabbix`
9. `sudo nano /etc/zabbix/zabbix_server.conf`
10. `systemctl restart zabbix-server apache2`
11. `systemctl enable zabbix-server apache2`
    
   ![изображение](https://github.com/sGolubn/Zabbix/blob/main/1.jpg)

### Задание 1

`Установите Zabbix Agent на два хоста.`
`Процесс выполнения.`

1. `Выполняя ДЗ, сверяйтесь с процессом отражённым в записи лекции.`
2. `Установите Zabbix Agent на 2 вирт.машины, одной из них может быть ваш Zabbix Server.`
3. `Добавьте Zabbix Server в список разрешенных серверов ваших Zabbix Agentов.`
4. `Добавьте Zabbix Agentов в раздел Configuration > Hosts вашего Zabbix Servera.`
5. `Проверьте, что в разделе Latest Data начали появляться данные с добавленных агентов.`
```
`Требования к результатам`

1.  `Приложите в файл README.md скриншот раздела Configuration > Hosts, где видно, что агенты подключены к серверу`
2.  `Приложите в файл README.md скриншот лога zabbix agent, где видно, что он работает с сервером`
3.  `Приложите в файл README.md скриншот раздела Monitoring > Latest data для обоих хостов, где видны поступающие от агентов данные.`
4.  `Приложите в файл README.md текст использованных команд в GitHub`

### Решение 2

1.  `sudo apt install zabbix-agent`
2.  `systemctl restart zabbix-agent`
3.  `systemctl enable zabbix-agent`
4.  `sed -i 's/Server=127.0.0.1/Server=192.168.1.36/g' /etc/zabbix/zabbix_agent.conf`
5.  `sed -i 's/Server=127.0.0.1/Server=192.168.1.33/g' /etc/zabbix/zabbix_agent.conf`

   ![изображение](https://github.com/sGolubn/Zabbix/blob/main/2.jpg).

   ![изображение](https://github.com/sGolubn/Zabbix/blob/main/3.jpg).

....

