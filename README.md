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
sudo dpkg-reconfigure wireshark-common # выбрать Yes
```
```bash
sudo adduser $USER wireshark
```
5. После добавления пользователя в группу неободимо перезагрузить нашу систему.

---

<h2 align="center">Установка <code>Neo4j</code></h2>

1. Открываем терминал Ubuntu и устанавливаем утилиту `curl`:
```bash
sudo apt install curl
```
2. Загружаем ключ безопасности для пакетов `Neo4j`, чтобы удостовериться в подлинности и целостности пакетов при их установке:
```bash
curl -fsSL https://debian.neo4j.com/neotechnology.gpg.key |sudo gpg --dearmor -o /usr/share/keyrings/neo4j.gpg
```
3. Добавляем репозиторий `Neo4j` в источники `APT` нашей системы:
```bash
echo "deb [signed-by=/usr/share/keyrings/neo4j.gpg] https://debian.neo4j.com stable 4.1" | sudo tee -a /etc/apt/sources.list.d/neo4j.list
```
4. Обновляем списки пакетов, после чего установливаем `Neo4j` и все его зависимости:
```bash
sudo apt update
```
```bash
sudo apt install neo4j
```

5. После установки `Neo4j` включим автозапуск при загрузке системы, запустим его и проверим его статус: 
```bash
sudo systemctl enable neo4j.service
```
```bash
sudo systemctl start neo4j.service
```
```bash
sudo systemctl status neo4j.service
```
6. Вызывем облочку `cypher-shell`, входим в систему и меняем пароль пользователю `neo4j` (по умолчанию: имя пользователя – neo4j, пароль – neo4j):
```bash
cypher-shell
```
```
:exit
```
7. После выполнения всех шагов можно пользоваться пользовательским интерфейсом `Neo4j` по адресу http://localhost:7474/ .
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
4. Смотрим стабильные доступные ветки (нас интересует ветка 4.4):
```bash
git branch -a
```
```bash
git checkout 4.4-stable
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

