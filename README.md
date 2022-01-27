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

Поиск файла в домашнем каиалоге
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

Получение информации с DNS сервера по доменому имени
```bash
host -a examle.com
host -v -t ANY examlle.com 
host -t NS example.com
host -t MX examle.com
host -t A examle.com
```

## Сертификаты LetsEncrypt
Установка certbot и модуля для nginx
```bash
sudo apt update
sudo apt install nginx
sudo apt install certbot python3-certbot-nginx
```

Создание wildcard сертификата с проверкой через TXT запись на сервере DNS
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












