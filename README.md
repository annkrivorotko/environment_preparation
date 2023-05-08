<h1 align="center">Подготовка окружения</h1>

<h2 align="center">Установка <code>Guest Addition</code></h2>

1. В `Ubuntu` открываем терминал и вводим команду:
```bash
sudo apt install dkms build-essential
```
2. Далее нажимаем на панели виртуальной машины `"Устройства"` и выбираем пункт `"Подключить образ диска Дополнений гостевой ОС..."`.
3. Появляется смонтированный образ, заходим в него, запускаем внутри терминал и пишем туда команду запуска:
```bash
./autorun.sh
```

4. Перезагружаем виртуальную машину.

---

<h2 align="center">Установка <code>Wireshark</code></h2>

1. Открываем в `Ubuntu` терминал и пишем команду для обновления списка пакетов:
```bash
sudo apt-get update 
```
2. Вводим команду  для установки `Wireshark`:
```bash
sudo apt-get install wireshark
```
3. После установки `Wireshark` доступен в меню приложений. 

---

<h2 align="center">Установка <code>PostgreSQL</code></h2>

1. Открываем в `Ubuntu` терминал и пишем команду для обновления списка пакетов:
```bash
sudo apt update
```
2. Устанавливаем `postgresql` и `postgresql-contrib`:
```bash
sudo apt install postgresql postgresql-contrib
```
3. Проверяем статус `postgresql`:
```bash
service postgresql status
```
4. Установливаем публичный ключ для репозитория (если это не было сделано ранее):
```bash
curl -fsS https://www.pgadmin.org/static/packages_pgadmin_org.pub | sudo gpg --dearmor -o /usr/share/keyrings/packages-pgadmin-org.gpg
```
5. Создаём файл конфигурации репозитория:
```bash
sudo sh -c 'echo "deb [signed-by=/usr/share/keyrings/packages-pgadmin-org.gpg] https://ftp.postgresql.org/pub/pgadmin/pgadmin4/apt/$(lsb_release -cs) pgadmin4 main" > /etc/apt/sources.list.d/pgadmin4.list && apt update'
```
6. Устанавливаем `pgadmin4`:
```bash
sudo apt install pgadmin4
```