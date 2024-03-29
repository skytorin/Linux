# Linux commands & utils

Удобное отображение размеров всех папок и файлов:
```bash
ncdu   
```                    

Удобный поиск и просмотр по истории команд:
```bash
hstr
```

Получить хэш от заданного текстового пароля по заданным параметрам:
```bash
mkpasswd --method=SHA-512 --rounds=4096
```

Показать все группы текущего пользователя без ID:
```bash
id -nG                  # Показать группы текущего пользователя
id -nG {user_name}      # Показать группы заданного пользователя
```

Частота процессора:
```bash
hwinfo --short --cpu           
watch hwinfo --short --cpu      # Автообновление информации
```

Датчики. Температура и обороты кулера:
```bash
sensors                                  # Вся информация по датчикам
watch "sensors | grep 'Core\|fan1:'"     # Обороты кулера
```

Монтирование диска Windows:
```bash
sudo apt install cifs-utils
sudo mount.cifs //192.168.8.11/d$ /mnt/d/ -o user=sergeev,domain=n.srv
sdptool browse 18:19:D6:C8:EF:E7
sdptool browse E5:0A:EF:F4:E7:60
```

Создать нагрузку на CPU:
```bash
md5sum /dev/urandom                      # Single thread CPU test
stress --cpu 4 --timeout 300s            # Multi threadCPU test
cat /dev/zero | bzip2 -c > /dev/null     # CPU Stress Test
```

Создать нагрузку на HDD:
```bash
cat /dev/sda3 | pipebench -q > /dev/null                          # RAW Read Speed Test
dd bs=16k count=102400 oflag=direct if=/dev/zero of=test_data     # Write Test
dd bs=16K count=102400 iflag=direct if=test_data of=/dev/null     # Read Test
```

Поиск файлов без учета регистра:
```bash
locate -i file
```

Поиск файла в домашнем каталоге:
```bash
find ~/ file
```

Вывод первых строк файла:
```bash
head /var/log/syslog              # вывод последних 10 строк
head -n 100 /var/log/syslog       # вывод последник 100 строк
```

Вывод последник строк файлов:
```bash
tail /var/log/syslog                           # вывод последних 10 строк
tail -n 100 /var/log/syslog                    # вывод последник 100 строк
tail -f /var/log/syslog                        # интерактивный режим
tail -f -s 5 /var/log/syslog                   # интерактивный режим с частотой обновления 5 секунд
tail -f --retry /var/log/syslog | grep error   # интерактивный режим с повтором открытия и фильтрацией по ошибкам
``` 

Вывод 5 самых больших по размеру  папок в текущей директории в порядке уменьшения размера:
```
sudo du -ahx . | sort -rh | head -5
```

Сравнение содержимого двух файлов:
```bash
diff file1 file2
```

Изменение фона экрана логина/блокировки в Kali Linux:
```bash
ln -s /usr/share/backgrounds/kali/kali-grub-16x9.png /usr/share/desktop-base/kali-theme/login/background
или
ln -s ../../../backgrounds/kali/kali-grub-16x9.png /usr/share/desktop-base/kali-theme/login/background
```

Получение информации с DNS сервера по доменному имени:
```bash
host -a examle.com            # Все DNS записи о хосте
host -t A examle.com          # Только A записи из DNS
host -t NS example.com        # Только NS записи из DNS
host -t MX examle.com         # Только MX записи из DNS
host -v -t ANY examlle.com    # Все записи
```

Вывод полных путей для всего содержимого каталога:
```bash
ls -d "$PWD"/* 
```

Цвет фона в консоли, выводимой командой ECHO:
```bash
echo -e "\033[40m - чёрный фон;\n\033[41m - красный фон;\n\033[42m - зелёный фон;\n\033[43m - желтый фон;\n\033[44m - синий фон;\n\033[45m - фиолетовый фон;\n\033[46m - голубой фон;\n\033[47m - серый фон;\n\033[0m - сброс фона на настройки по умолчанию"
```

Цвет текста в консоли, выводимой командой ECHO:
```bash
echo -e "\033[41m\033[30m - чёрный текст;\033[0m\n\033[0m\033[31m - красный текст;\n\033[32m - зелёный текст;\n\033[33m - желтый текст;\n\033[34m - синий текст;\n\033[35m - фиолетовый текст;\n\033[36m - голубой текст;\n\033[37m - серый текст\n"
```


## SYSTEMD / Systemctl
```
systemctl --type=service
systemctl list-units --type=service
systemctl --type=service --state=active
systemctl list-units --type=service --state=active
systemctl --type=service --state=running
systemctl list-units --type=service --state=running 
systemctl start service
systemctl stop service
systemctl status service
systemctl restart service
```


## GREP

Выведет все строки, содержащие заданные символы, без учета регистра:
```bash
cat file.txt | grep -i "text"
```

Выведет все строки, начинающиеся с символа комментария #:
```bash
cat file.txt | grep "^#"
```

Выведет все строки, которые не являются пустыми:
```bash
cat file.txt | grep -v "^$"
```

Поиск по всем файлам c расширением log и вывод строк начинающихся с символа #: 
```bash
grep "^#" /var/*.log
```

Вывод количества найденных совпадений по каждлому файлу в отдельности:
```bash
grep -с "text" /var/*.log
```

Выведет все строки, содержащие заданные символы, с указанием номера строки:
```bash
grep -n "text" /var/*.log
```

Выведет только названия файлов, содержащие заданные символы:
```bash
grep -l "text" /var/*.log
```

Выведет только абсолютно совпадающие строки:
```bash
grep -x "text" /var/messages.log
```

Выведет только строки, содерщащие точку в конце строки:
```bash
grep "\.$" /var/messages.log
```

Выведет строки, совпадающие с символами указанными в файле шаблона:
```bash
grep -f pattern.txt /var/messages.log
```

Выведет строки, совпадающие с символами указанными в нескольких файлах шаблонов:
```bash
grep -e pattern1.txt -e pattern2.txt -e pattern3.txt /var/messages.log
```

Использование расширенных регулярных выражений egre или -E.
Выведет строки начинающиеся с символов # или $:
```bash
grep -E '^#|$' /var/messages.log 
 или
egrep '^#|$' /var/messages.log 
```

Выведет все строки, содержащие заданные символы и 3 нежестоящих строки:
```bash
grep -A 3 "text" /var/*.log
```

Выведет все строки, содержащие заданные символы и 3 вышестоящие строки:
```bash
grep -B 3 "text" /var/*.log
```


## SED

Опции, которые могут пригодиться для создания скрипта:
```bash
-s   # замена шаблона выражений 
-y   # замена шаблона символов 
-d   # удаление строк
-i   # вставка перед указанной строкой
-а   # вставка текста после указанной строки
```

Вывод на экран содержимого файла без строк начинающихся с # и пустых строк:
```bash
sed -e '/^#/d; /^$/d' file.txt
 или
sed -e '/^#/d' -e '/^$/d' file.txt
```

Заменит во всем файле выражение Windows на Linux:
```bash
sed 's/Windows/Linux/g' test4_copy.log
```

Заменит только в третьей строке файла выражение Windows на Linux и выведет это на экран, также сохранит измененную строку в новом файле:
```bash
sed '3s/Windows/Linux/w file_copy.txt' file.txt
```


## AWK

Вывод интерпритаторов всех пользователей, указанных в файле /etc/passwd:
```bash
awk -F: '{print $7}' /etc/passwd
```

Вывод только тех строк в которых есть цифры:
```bash
awk '/[[:digit:]]/{print $0}' file.txt
```

Вывод заданной колонки:
```bash
awk 'END { print "The file contains", NR, "lines"}' file.txt
```

Вывод кол-ва строк в файле:
```bash
awk 'END { print "The file contains", NR, "lines"}' file.txt
```

Замена слова в первой позиции с последующим выводом:
```bash
echo "Moscow is the capital of GB" | awk '{$1="London"; print $0}'
```

Структурирование строк на блоки в зависимости от кол-ва знаков и вывод необходимых блоков в заданном порядке:
```bash
cat file.txt
redhat ubuntu centos debian fedora kali
awk 'BEGIN {FIELDWIDTHS="6 1 6 1 6 1 6 1 6 1 4"} {print $7, $3, $11}' file.txt
debian ubuntu kali
```

Берет из файла /etc/passwd только 1 и 3 поле, после чего выводит пользователей, чей ID > 99:
```bash
cut -d: -f1,3 /etc/passwd | awk -F: '$2 > 99 {print $1}'
```

Вывод только первого столбца из файла:
```bash
gawk -F: '{ print $1 }' /etc/passwd
```

## CURL

Проверка заголовков и кода ответа:
```
curl -I -k https://yandex.ru     # ключ -k игнорирует сертификат https
```

Проверка только кода ответа:
```
curl -I -k https://yandex.ru 2>/dev/null | head -n 1 | cut -d$' ' -f2
```

Проверка ответа почтового SMTP
```
curl -v smtp.yandex.ru:25
```


## TCPDUMP

Снять весь трафик с интерфейса eth0:
```
tcpdump –i eth0
```

Снять трафик на интерфейсе eth0, на порту 22:
```
sudo tcpdump -i eth0 port 22
```

Снять трафик на интерфейсе eth0, по протоколу tcp на порту 22:
```
sudo tcpdump -i eth0 tcp port 22
```

Снять трафик с диапазона портов на интерфейсе eth0:
```
sudo tcpdump -i eth0 portrange 100-200
```

Снять трафик на интерфейсе eth0, идущий от хоста 192.168.10.2:
```
sudo tcpdump -i ens3 host 192.168.10.2
```

Снять весь трафик, идущий к 192.168.10.1, который не является ICMP:
```
sudo tcpdump dst 192.168.10.1 and not icmp
```

Запись вывода в файл:
```
sudo tcpdump -w sshtrace.tcpdump port 22
```

Ловим весь входящий трафик, исключая трафик генерируемый нашей SSH-сессией:
```
sudo tcpdump -i eth0 -n -nn -ttt 'dst host 192.168.10.1 and not ( src host 192.168.10.2 and dst port 22 )'
```


## Пакетный менеджер APT

Обновления кэша с информацией о пакетах:
```bash
sudo apt update
```

Просмотр всех пакетов, которые будут обновлены:
```bash
apt list --upgradable
```

Обновление пакетов:
```bash
sudo apt install telegram-desktop --reinstall
sudo apt install chromium --reinstall
sudo apt install firefox-esr --reinstall
```

Обновление системы Linux до последней версии (ядро и все пакеты):
```bash
sudo apt update && sudo apt full-upgrade -y
```

Удаление неиспользуемых пакетов и ядер:
```bash
sudo apt autoremove -y
```

Очистка кэша пакетов:
```bash
sudo apt autoclean -y
```


## SSH

Директории SSH:
```bash
/etc/ssh/sshd_config            # конфиг демона SSH
~/.ssh                          # скрытая служебная директория ssh в директории пользователя 
~/.ssh/authorized_keys          # файл с открытыми ключами  
```

Рекомендуемые изменения в конфиге демона:
```bash
Port                            # смена порта, где располагается служба по умолчанию  
PubkeyAuthentication yes        # включение авторизации по ssh-ключам  
PermitEmptyPasswords no         # запрет использования пустых паролей
PasswordAuthentication no       # запрет авторизации по паролю в принципе 
```

Опционально:
```bash
ListenAddress 188.120.242.XXX   # указываем конкретный IP, на котором будет располагаться служба. По умолчанию на всех  
UseDNS yes                      # проверка соответствия DNS-имени IP-адресу клиента
MaxAuthTries 3                  # количество неудачных попыток подключения
PermitEmptyPasswords no         # запрет пустых паролей
PermitRootLogin no              # запрет авторизации пользователя root  
AllowUsers User1 User2          # разрешение на подключение конкретных пользователей 
AllowGroups Group1, Group2      # доступ определенным группам
AllowTcpForwarding yes          # разрешение переадресации TCP для организации SSH tunnel
GatewayPorts yes                # еренаправление удаленных портов, по умолчанию отключено
Login GraceTime 30              # время, в течении которого система ожидает от пользователя ввода пароля
ClientAliveInterval 300         # Отключение пользователя при бездействии
```
Копирование ssh-ключей на удаленный сервер:
```bash
ssh-copy-id -i ~/.ssh/id_rsa.pub user@remote_host 
```

### SSH Tunnel
Переадресация локального порта 1111 на удаленный порт 5432:
```
ssh -f -N user@remote_host -L 1111:remote_host:5432
```

Переадресация удаленного порта 5000 на локальный порт 3000:
```
ssh -f -N user@remote_host -R 5000:local_host:3000
```

Запустить прокси-сервер SOCKS на порту 1080:
```
ssh -f -N -D 1080 user@remote_host
```
Опции
```
-L    # переадресация локального порта на удаленный порт
-R    # переадресация удаленного порта на локальный порт
-D    # динамическая переадресация портов, аналог прокси-сервера SOCKS
-f    # работать в фоновом режиме
-N    # не выполнять удаленную команду, в этом случае не будет оболочки
```


## Сертификаты LetsEncrypt
Установка certbot и модуля для nginx:
```bash
sudo apt update
sudo apt install nginx
sudo apt install certbot python3-certbot-nginx
```

Создание WildCard сертификата с проверкой через TXT запись на сервере DNS:
```bash
certbot certonly -d *.example.com --manual --preferred-challenges dns
```


## IPTABLES / UFW

Установка и настройка брандмауэра с использованием UFW:
```
sudo apt install ufw
ufw enable
ufw disable
sudo ufw reset
sudo ufw status verbose
sudo ufw status numbered
sudo ufw delete 2
sudo ufw delete allow http
sudo ufw allow 6000:6007/tcp
sudo ufw allow 6000:6007/udp
sudo ufw allow from 203.0.113.4
sudo ufw allow from 203.0.113.0/24
sudo ufw allow from 203.0.113.4 to any port 22
sudo ufw allow from 203.0.113.0/24 to any port 22
sudo ufw allow in on eth0 to any port 80
sudo ufw deny http
sudo ufw deny from 203.0.113.4
```

Команды iptables
```
iptables -A INPUT -p tcp -d 10.10.0.1  --dport 22 -j ACCEPT
iptables --line-numbers -L -v -n | grep :22
iptables -D INPUT 5
```


## Горячие клавиши в Shell  

Сочетания с клавишей Ctrl: 
```bash
Ctrl + a  # переход в начало строки (cisco, csh, zsh)  
Ctrl + b  # переход на 1 символ назад (cisco, csh, zsh)  
Ctrl + c  # посылает программе SIGINT. Обычно, прерывает текущее задание (csh, zsh)  
Ctrl + d  # удаляет символ под курсором (аналог delete) (cisco, csh, zsh)  
Ctrl + e  # переход к концу строки (cisco, csh, zsh)  
Ctrl + f  # переход на 1 символ вперёд (cisco, csh, zsh)  
Ctrl + k  # удаляет всё, до конца строки (EOL, а не на экране!) (cisco, csh, zsh)  
Ctrl + l  # очищает экран. Аналог команды clear. (csh, zsh)  
Ctrl + r  # поиск по истории. Повторение поиска (листание результатов поиска). То есть инкрементальный поиск. (zsh)  
Ctrl + j  # прекращает поиск и позволяет отредактировать найденную команду. Если поиск не производился, то аналогично нажатию return. (в zsh выполняет команду)  
Ctrl + t  # меняет символ под курсором на предыдущий. Или, если хотите, тянет предыдущий символ к концу строки. (cisco, csh, zsh)  
Ctrl + u  # удаляет все символы слева от курсора до начала строки. (cisco, в csh, zsh удаляет всю строку)  
Ctrl + w  # удаляет символы слева от курсора до начала слова. (cisco, csh, zsh)  
Ctrl + z  # suspend'ит текущую задачу (csh, zsh)  
Ctrl + xx  # переходит от текущей позиции курса в начало строки и обратно. На циске работает аналогично ctrl + u. (csh)  
Ctrl + x @  # показывает возможные дополнения имени хоста (имена берутся из /etc/hosts)  
Ctrl + x; Ctrl + e  # открывает $EDITOR для изменения введённой строки. После сохранения изменений, команда отправляется на исполнение.  
```

Сочетания с клавишей Alt:
```bash
Alt + <  # переход к первой команде в истории команд (zsh)  
Alt + >  # переход к последней команде в истории  
Alt +?   # показывает список возможных дополнений команды(аналогично tab-tab) (в csh, zsh аналог which string)  
Alt + *  # вставляет все возможные дополнений команды в строку команд  
Alt + /  # пытается дополнить имя файла (аналогично табуляции)  
Alt +.   # вставляет последний аргумент предыдущей команды (аналог !$, только не надо делать :p, чтобы проверить )  
Alt + b  # сдвигает курсор влево на 1 слово (cisco, csh, zsh)  
Alt + c  # делает букву под курсором большой, а остальные, до конца слова, маленькими. (cisco, csh, zsh)  
Alt + d  # удаляет символы с текущей позиции курсора и до конца слова. (cisco, csh, zsh)  
Alt + f  # передвигает курсор на одно слово вперёд (cisco, csh, zsh)  
Alt + l  # делает все буквы с текущей позиции курсора и до конца слова маленькими (cisco, csh, zsh)  
Alt + t  # меняет местами слова под курсором и предыдущее (zsh)  
Alt + u  # переводит буквы с текущей позиции курсора и до конца слова в верхний регистр (cisco, csh, zsh)  
Alt + back-space # удаляет символы с текущей позиции курсора до начала слова (cisco, csh, zsh)  
```

Сочетания с двойным нажатием клавиши табуляции (Tab) (обозначено как «2Т»):  
```bash
2T   # при пустой строке, выведет список всех доступных команд  
*2T  # покажет подпапки исключая скрытые (имена которых начинаются с точки)  
~2T  # выведет всех пользователей из /etc/passwd. Дополнив имя пользователя можно перейти в его домашний каталог.   
$2T  # выводит список дополнений для системных переменных  
@2T  # дополняет имена хостов содержащимися в /etc/hosts  
=2T  # листинг текущей директории, аналогичный ls  
(dir)2T  # покажет подпапки папки dir
(string)2T  # выведет список возможных дополнений  
```


## Перенаправление ввода/вывода

```bash
0 - stdin     # стандартный ввод (клавиатура)  
1 - stdout    # стандартный вывод (экран)  
2 - stderr    # стандартная ошибка (вывод ошибок на экран)  
```

Вывод всех сообщений в лог:
```bash
cat file &> log 
```

Вывод только ошибок в лог:
```bash
cat file 2> log
```

## Запуск нескольких команд за раз

Запуск нескольких команд последовательно (;):
```bash
echo -n "Hello, "; echo "World!"
```

Запуск нескольких зависимых друг от друга команд (&&):
```bash
echo -n "Hello, " && echo "World!"
```

Запуск следующей команды при условии, что первая команда не выполнилась (||):
```bash
wrongCommand || echo "Запуск, если первая команда не выполнилась"
```

Параллельный запуск нескольких команд:
```bash
(echo "Первая команда" &); (echo "Вторая команда" &)
```


## Выполнение команд в фоновом режиме

Запуск команды в фоновом режиме:
```bash
sleep 3600 &
```

Запуск команды в фоновом режиме и вывод ошибок в лог файл:
```bash
sleep 3600 2>>error.log &
```

Чтобы перевести в фон активный процесс, нужно его приостановить выполнения сочетанием Ctrl + Z и ввести в консоли команду bg: 
```bash
bg
```

Список команд, запущенных в фоновом режиме:
```bash
jobs -l
```

Фоновый режим привязан к сессии — при выходе из терминала все процессы, запущенные через него, будут прерваны. Этого можно избежать, использую команду через nohup:
```bash
nohup sleep 3600 &
```

Отвязать от сессии уже запущенный процес можно командой disown:
```bash
disown -h %ID
```

Вернуть процесс на передний план можно командой fg:
```bash
fg 
```
или если фоновых процессов несколько, то нужно указать ID:
```bash
fg %ID
```

тмена процесса, запущенного в фоновом режиме, выполняется командой:
```bash
kill PID
```

Если процесс завис, то нужно использовать более грубый вариант:
```bash
kill -KILL PID
 или
kill -9 PID
```


## VI / VIM

Включить/выключить нумерацию строк:
```bash
set number / :set nonumber
```
### Основные команды перемещения по тексту
Перейти к строке с номером
```bash
(esc):номер или (esc),номер,shift+g
```

Поиск по тексту
```bash
(esc)/слово_которое_ищем   # поиск слов в прямом направлении
(esc)?слово_которое_ищем   # поиск слов в обратном направлении
(esc) shift+j              # в конце строки объединит строки вместе.
(esc) shift+g              # переместит в конец текста
```

Перемещение на первый символ в режиме просмотра
```bash
1g
```

### Работа с буфером
```bash
(esc) dd    # удалить (вырезать) строку в буфер
(esc) 10dd  # удалить (вырезать) 10 строк в буфер
(esc) yy    # скопировать строку в буфер
(esc) 10yy  # скопировать 10 строк в буфер
(esc) p     # вставить содержимое буфера под курсором
(esc) P     # вставить содержимое буфера над курсором
```

### Замена текста
```bash
(esc):s/что_меняем/на_что_меняем/g
```
g - обозначает замену до конца строки

если надо менять по всему файлу, то тогда пишем
```bash
(esc):%s/что_меняем/на_что_меняем/g
```

Комментировать блок текста от курсора до строки номер 10
```bash
:.,10s/^/#/
```

Комментировать блок текста от курсора до конца:
```bash
:.,$/^/#/
```

### Выход из редактора
Выход осуществляется последовательностью нажатий:
```bash
(esc):q
```

Выход без сохранения:
```bash
(esc):q!
```

Выход с сохранением текста:
```bash
(esc):wq или (esc):exit
```

Выход с принудительным сохранением (например, если файл read-only):
```bash
(esc):wq!
```
