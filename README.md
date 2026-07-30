# Домашнее задание к занятию "`Название занятия`" - `Илембетов Василь`

---

### Задание 1

```
Установите и сконфигурируйте Zabbix для выбранной платформы Zabbix 7, Ubuntu 24.04, Server, Frontend, Agent, PostgreSQL, Apache

a. Become root user
Start new shell session with root privileges.

$ sudo -s


b. Установите репозиторий Zabbix
Документация
# wget https://repo.zabbix.com/zabbix/7.0/ubuntu/pool/main/z/zabbix-release/zabbix-release_latest_7.0+ubuntu24.04_all.deb
# dpkg -i zabbix-release_latest_7.0+ubuntu24.04_all.deb
# apt update



c. Установите Zabbix сервер, веб-интерфейс и агент
# apt install zabbix-server-pgsql zabbix-frontend-php php8.3-pgsql zabbix-apache-conf zabbix-sql-scripts zabbix-agent



d. Создайте базу данных
Установите и запустите сервер базы данных.
Выполните следующие комманды на хосте, где будет распологаться база данных.
# sudo -u postgres createuser --pwprompt zabbix
# sudo -u postgres createdb -O zabbix zabbix


На хосте Zabbix сервера импортируйте начальную схему и данные. Вам будет предложено ввести недавно созданный пароль.
# zcat /usr/share/zabbix-sql-scripts/postgresql/server.sql.gz | sudo -u zabbix psql zabbix



e. Настройте базу данных для Zabbix сервера
Отредактируйте файл /etc/zabbix/zabbix_server.conf
DBPassword=password


f. Запустите процессы Zabbix сервера и агента
Запустите процессы Zabbix сервера и агента и настройте их запуск при загрузке ОС.
# systemctl restart zabbix-server zabbix-agent apache2
# systemctl enable zabbix-server zabbix-agent apache2


g. Open Zabbix UI web page
The default URL for Zabbix UI when using Apache web server is http://127.0.0.1/zabbix


```

`При необходимости прикрепитe сюда скриншоты
![скриншот авторизации в админке](img/скриншот авторизации в админке.png)`


---

### Задание 2

```
Настройка на стороне второго сервера (130.193.58.204)

sudo -s
# Скачивание и установка репозитория Zabbix 7.0
wget https://repo.zabbix.com/zabbix/7.0/ubuntu/pool/main/z/zabbix-release/zabbix-release_latest_7.0+ubuntu24.04_all.deb
dpkg -i zabbix-release_latest_7.0+ubuntu24.04_all.deb
apt update

# Установка агента
sudo apt install zabbix-agent


# Настройка конфигурации (указание DDNS-имени сервера и Hostname)
sudo nano /etc/zabbix/zabbix_agentd.conf
# Внутри файла изменили: Server=0.0.0.0/0, ServerActive=имя_сервера.ddns.net

# Перезапуск и добавление агента в автозагрузку
systemctl restart zabbix-agent
systemctl enable zabbix-agent

# Проверка логов для отчета
tail -n 20 /var/log/zabbix/zabbix_agentd.log

Настройка в веб-интерфейсе Zabbix
Перешли в Data collection -> Hosts -> Create host.
Указали Host name (Ubuntu-Client), привязали активный шаблон Linux by Zabbix agent active и вписали IP-адрес хоста.
Проверили поступление метрик в разделе Monitoring -> Latest data.


```

`При необходимости прикрепитe сюда скриншоты
![Название скриншота 2](ссылка на скриншот 2)`


---

### Задание 3

```
В официально сайте находим продукт для установки Zabbix-агента, выбираем конфигурацию, и скачиваем файл установщика для Windows.
Далее при установке прописываем данные Zabbix-сервера.

В файле C:\Program Files\Zabbix Agent\zabbix_agentd.conf перевели агента в активный режим работы на локальный адрес проброса
Перезапустили службу Zabbix Agent в Windows через оснастку служб


Настройка в веб-интерфейсе Zabbix
Перешли в Data collection -> Hosts -> Create host
Указали Host name (Windows_home), привязали активный шаблон Windows by Zabbix agent active и вписали IP-адрес хоста.
Проверили поступление метрик в разделе Monitoring -> Latest data.


```

`При необходимости прикрепитe сюда скриншоты
![Название скриншота](ссылка на скриншот)`

