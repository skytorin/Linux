# Linux commands
Частота процессора:
```bash
watch hwinfo --short --cpu
hwinfo --short --cpu
```

Температуры и обороты кулера:
```bash
sensors
watch "sensors | grep 'Core\|fan1:'" 
```

Монтирование диска Windows:
```bash
sudo apt install cifs-utils
sudo mount.cifs //192.168.8.11/d$ /mnt/d/ -o user=sergeev,domain=n.srv
sdptool browse 18:19:D6:C8:EF:E7
sdptool browse E5:0A:EF:F4:E7:60
```

Создать нагрузку на CPU
```bash
md5sum /dev/urandom - Single thread CPU test
stress --cpu 4 --timeout 300s - Multi threadCPU test
cat /dev/zero | bzip2 -c > /dev/null - CPU Stress Test
```
Создать нагрузку на HDD
```bash
cat /dev/sda3 | pipebench -q > /dev/null - RAW Read Speed Test
dd bs=16k count=102400 oflag=direct if=/dev/zero of=test_data - Write Test
dd bs=16K count=102400 iflag=direct if=test_data of=/dev/null - Read Test
```

Обновления кэша с информацией о пакетах
```bash
sudo apt update
```

Просмотр всех пакетов, которые будут обновлены
```bash
apt list --upgradable
```

Обновление пакетов
```bash
sudo apt install telegram-desktop --reinstall
sudo apt install chromium --reinstall
sudo apt install firefox-esr --reinstall
```

Обновление системы Linux до последней версии (ядро и все пакеты)
```bash
sudo apt update && sudo apt full-upgrade -y
```

Удаление неиспользуемых пакетов и ядер
```bash
sudo apt autoremove -y
```

Очистка кэша пакетов
```bash
sudo apt autoclean -y
```

Поиск файлов без учета регистра
```bash
locate -i file
```

Поиск файла в домашнем каталоге
```bash
find ~/ file
```
Вывод 20 первых строк файла
```bash
head -n 20 file1
```

Вывод 20 последних строк файла
```bash
tail -n 20 file2
```

Сравнение содержимого двух файлов
```bash
diff file1 file2
```

Изменение фона экрана логина/блокировки в Kali Linux
```bash
ln -s /usr/share/backgrounds/kali/kali-grub-16x9.png /usr/share/desktop-base/kali-theme/login/background
или
ln -s ../../../backgrounds/kali/kali-grub-16x9.png /usr/share/desktop-base/kali-theme/login/background
```

Получение информации с DNS сервера по доменному имени
```bash
host -a examle.com
host -v -t ANY examlle.com 
host -t NS example.com
host -t MX examle.com
host -t A examle.com
```

## SSH
/etc/ssh/sshd_config — конфиг демона SSH.

Рекомендуемые изменения в конфиге демоне:

Port — смена порта, где располагается служба по умолчанию.
PubkeyAuthentication yes — включение авторизации по ssh-ключам.
PermitEmptyPasswords no — запрет использования пустых паролей.
PasswordAuthentication no — запрет авторизации по паролю в принципе.

Опционально
ListenAddress 188.120.242.XXX — указываем конкретный IP, на котором будет располагаться служба. По умолчанию на всех.
PermitRootLogin no — запрет авторизации пользователя root.
AllowUsers User1 User2 — разрешение на подключение конкретных пользователей.

~/.ssh - скрытая служебная директория ssh в директории пользователя.
~/.ssh/authorized_keys — файл с открытыми ключами.
ssh-copy-id — команда для копирования ssh-ключей на удаленный сервер.

## Сертификаты LetsEncrypt
Установка certbot и модуля для nginx
```bash
sudo apt update
sudo apt install nginx
sudo apt install certbot python3-certbot-nginx
```

Создание WildCard сертификата с проверкой через TXT запись на сервере DNS
```bash
certbot certonly -d *.example.com --manual --preferred-challenges dns
```

Вывод полных путей для всего содержимого каталога
```bash
ls -d "$PWD"/* 
```

Цвет фона в консоли, выводимой командой ECHO
```bash
echo -e "\033[40m - чёрный фон;\n\033[41m - красный фон;\n\033[42m - зелёный фон;\n\033[43m - желтый фон;\n\033[44m - синий фон;\n\033[45m - фиолетовый фон;\n\033[46m - голубой фон;\n\033[47m - серый фон;\n\033[0m - сброс фона на настройки по умолчанию"
```

Цвет текста в консоли, выводимой командой ECHO
```bash
echo -e "\033[41m\033[30m - чёрный текст;\033[0m\n\033[0m\033[31m - красный текст;\n\033[32m - зелёный текст;\n\033[33m - желтый текст;\n\033[34m - синий текст;\n\033[35m - фиолетовый текст;\n\033[36m - голубой текст;\n\033[37m - серый текст\n"

```
Вывод последник строк файлов
```bash
tail /var/log/syslog              # вывод последних 10 строк
tail -n 100 /var/log/syslogtail   # вывод последник 100 строк
tail -f /var/log/syslog           # интерактивный режим
tail -f -s 5 /var/log/syslog      # интерактивный режим с частотой обновления 5 секунд
tail -f --retry /var/log/syslog | grep error  # интерактивный режим с повтором открытия и фильтрацией по ошибкам
``` 


## Горячие клавиши в shell
Сочетания с клавишей Ctrl
Ctrl + a - переход в начало строки (cisco, csh, zsh)
Ctrl + b - переход на 1 символ назад (cisco, csh, zsh)
Ctrl + c - посылает программе SIGINT. Обычно, прерывает текущее задание (csh, zsh)
Ctrl + d - удаляет символ под курсором (аналог delete) (cisco, csh, zsh)
Ctrl + e - переход к концу строки (cisco, csh, zsh)
Ctrl + f - переход на 1 символ вперёд (cisco, csh, zsh)
Ctrl + k - удаляет всё, до конца строки (EOL, а не на экране!) (cisco, csh, zsh)
Ctrl + l - очищает экран. Аналог команды clear. (csh, zsh)
Ctrl + r - поиск по истории. Повторение поиска (листание результатов поиска). То есть инкрементальный поиск. (zsh)
Ctrl + j - прекращает поиск и позволяет отредактировать найденную команду. Если поиск не производился, то аналогично нажатию return. (в zsh выполняет команду)
Ctrl + t - меняет символ под курсором на предыдущий. Или, если хотите, тянет предыдущий символ к концу строки. (cisco, csh, zsh)
Ctrl + u - удаляет все символы слева от курсора до начала строки. (cisco, в csh, zsh удаляет всю строку)
Ctrl + w - удаляет символы слева от курсора до начала слова. (cisco, csh, zsh)
Ctrl + xx - переходит от текущей позиции курса в начало строки и обратно. На циске работает аналогично ctrl + u. (csh)
Ctrl + x @ - показывает возможные дополнения имени хоста (имена берутся из /etc/hosts)
Ctrl + z - suspend'ит текущую задачу (csh, zsh)
Ctrl + x; Ctrl + e - открывает $EDITOR для изменения введённой строки. После сохранения изменений, команда отправляется на исполнение.

Сочетания с клавишей Alt
Alt + < - переход к первой команде в истории команд (zsh)
Alt + > - переход к последней команде в истории
Alt +? - показывает список возможных дополнений команды(аналогично tab-tab) (в csh, zsh аналог which string)
Alt + * - вставляет все возможные дополнений команды в строку команд
Alt + / - пытается дополнить имя файла (аналогично табуляции)
Alt +. - вставляет последний аргумент предыдущей команды (аналог !$, только не надо делать :p, чтобы проверить )
Alt + b - сдвигает курсор влево на 1 слово (cisco, csh, zsh)
Alt + c - делает букву под курсором большой, а остальные, до конца слова, маленькими. (cisco, csh, zsh)
Alt + d - удаляет символы с текущей позиции курсора и до конца слова. (cisco, csh, zsh)
Alt + f - передвигает курсор на одно слово вперёд (cisco, csh, zsh)
Alt + l - делает все буквы с текущей позиции курсора и до конца слова маленькими (cisco, csh, zsh)
Alt + t - меняет местами слова под курсором и предыдущее (zsh)
Alt + u - переводит буквы с текущей позиции курсора и до конца слова в верхний регистр (cisco, csh, zsh)
Alt + back-space - удаляет символы с текущей позиции курсора до начала слова (cisco, csh, zsh)

Сочетания с двойным нажатием клавиши табуляции (Tab) (обозначено как «2Т»)
Если нажать при пустой строке — выведет список всех доступных команд
(string)2T - выведет список возможных дополнений
(dir)2T - покажет подпапки папки dir
*2T - покажет подпапки исключая скрытые (имена которых начинаются с точки)
~2T - выведет всех пользователей из /etc/passwd. Дополнив имя пользователя можно перейти в его домашний каталог. Например ~oxpa/ — домашний каталог пользователя oxpa
$2T - выводит список дополнений для системных переменных
@2T - дополняет имена хостов содержащимися в /etc/hosts
=2T - листинг текущей директории, аналогичный ls.







