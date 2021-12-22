#### Если на одном ПК стоит и виндовс и линукс, и время в виндовс постоянно сбивается (при этом в линуксе правильное).
Чтобы Линукс не переводил часы на «+0», делаем
```
timedatectl set-local-rtc 1
```
и если вдруг нужно будет вернуть все назад
```
timedatectl set-local-rtc 0
```
#### Изменить время выбора системы или ядра при загрузке
ищем `/etc/default/grub` меняем в строчке `GRUB_TIMEOUT=` цифру ожидания в сек на желаемую

#### Определить, обновить драйвер на видеокарту Nvidia
Как определило ядро
```
lspci -nn | grep VGA
```

Добавим репозиторий с драйверами
```
sudo add-apt-repository ppa:graphics-drivers/ppa
sudo apt update
```

Определение подходящих драйверов
```
sudo ubuntu-drivers devices
```

И установка (название из предыдущего пункта)
```
sudo apt install nvidia-driver-440
```
#### Команды консоли для развертывания проекта

Сменить владельца всего в текущей папке рекурсивно
```
chown -R fastuser:fastuser *
```

Сменить права на папки
```
find . -type d -exec chmod 0755 {} \;
```
Сменить права на файлы
```
find . -type f -exec chmod 0644 {} \;
```

Поиск файлов. измененных в последние 3 дня (напр. после вируса)
```
find /var/adm -mtime +3 -print
```

Архивация проекта с исключением ненужного (. - текущая папка)
```
tar -zcpvf archive.tar.gz --anchored --exclude=./_old --exclude=./runtime .
```
еще вариант
```
tar -zcpvf archive.tar.gz --anchored --exclude={./.git,'*/runtime/*','*/assets/*','*/uploads/*','*/web/images/*',./vendor/*,'*/temp/*',./console/images_fix,*.tgz,*.gz,*.zip,*.xls} .
```
