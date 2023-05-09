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

4. Для того чтобы наш пользователь мог работать с `Wireshark` необходимо добавить пользователя в группу:
```bash
sudo dpkg-reconfigure wireshark--common # выбрать Yes
```
```bash
sudo adduser $USER wireshark
```
5. После добавления пользователя в группу неободимо перезагрузить нашу систему.

---

<h2 align="center">Установка <code>PostgreSQL</code> и <code>pgAdmin4</code></h2>

<h3 align="center">PostgreSQL</h3>

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
4. Сразу установим пароль для пользователя `postgres`:
```bash
sudo -u postgres psql postgres # заходим в PostgreSQL shell
```
```bash
\password postgres # меняем пароль для postgres
```
```bash
\q # выходим из PostgreSQL shell
```



<h3 align="center">pgAdmin4</h3>

1. Устанавливаем утилиту `curl`:
```bash
sudo apt install curl
```
2. Установливаем публичный ключ для репозитория:
```bash
curl -fsS https://www.pgadmin.org/static/packages_pgadmin_org.pub | sudo gpg --dearmor -o /usr/share/keyrings/packages-pgadmin-org.gpg
```
3. Создаём файл конфигурации репозитория:
```bash
sudo sh -c 'echo "deb [signed-by=/usr/share/keyrings/packages-pgadmin-org.gpg] https://ftp.postgresql.org/pub/pgadmin/pgadmin4/apt/$(lsb_release -cs) pgadmin4 main" > /etc/apt/sources.list.d/pgadmin4.list && apt update'
```
4. Устанавливаем `pgadmin4`:
```bash
sudo apt install pgadmin4
```
5. После установки `pgAdmin4` доступен в меню приложений. 

---

<h2 align="center">Установка <code>nDPI</code></h2>

1. Заходим в теминал `Ubuntu` (Ctrl + Alt + T).

2. Устанавливаем необходимые зависимости для компиляции и установки библиотеки `nDPI` с помощьщию команды:
```bash
sudo apt-get install build-essential git gettext flex bison libtool autoconf automake pkg-config libpcap-dev libjson-c-dev libnuma-dev libpcre2-dev libmaxminddb-dev librrd-dev
```
3. Клонируем репозиторий с исходным кодом библиотеки `nDPI`, после чего переходим в склонированный репозиторий:
```bash
git clone https://github.com/ntop/nDPI.git
```
```bash
cd nDPI
```
4. Смотрим доступные ветки, чтобы найти последнюю стабильную версию `nDPI`, и переходим на эту ветку:
```bash
git branch -a
```
```bash
git checkout 4.6-stable
```
5. Устанавливаем `nDPI` в нашу систему
```bash
./autogen.sh
```
```bash
./configure
```
```bash
make
```
```bash
sudo make install
```
6. Проверим что установка `nDPI` прошла успешно:
```bash
ndpiReader -v
```

