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

Изменение фона экрана логина/блокировки в Kali Linx
```bash
ln -s /usr/share/backgrounds/kali/kali-grub-16x9.png /usr/share/desktop-base/kali-theme/login/background
или
ln -s ../../../backgrounds/kali/kali-grub-16x9.png /usr/share/desktop-base/kali-theme/login/background
```

