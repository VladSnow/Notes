## Установка Raspberry Pi для работы с smartRTU
**Документация по установки [smartRTU](https://github.com/RTUDF/smartRTU) с нуля на Raspberry Pi**  

## Содержание
* [Ставим Raspbian на Raspberry Pi](#chapter-0)  
* [Настройка raspi-config](#chapter-1)  
* [Установка нужных пакетов](#chapter-2)  
* [Установка и проверка openVG](#chapter-3)  
* [Настройка статичного ip](#chapter-4)

<a id="chapter-0"></a>  

## Ставим Raspbian на Raspberry Pi
* Для создания образа нам нужна будет программа **Win32 Disk Imager** - [скачать Win32](https://sourceforge.net/projects/win32diskimager/)  
* И сам [образ Raspbian](https://www.raspberrypi.org/downloads/raspbian/)  
Качаем полную версию: RASPBIAN STRETCH WITH DESKTOP  

После записи образа на micro SD вставляем ее в Raspberry Pi и приступаем к настройке  

<a id="chapter-1"></a>  

## Настройка raspi-config
Заходим в raspi-config `sudo raspi-config` и настраиваем его  
* отключение автозапуска window-x    
  * boot options
  * Deskctop / CLI
  * Console  
* дать допуск работы с ssh  
  * Interfacing Options
  * SSH
    * Enabled (YES)  
* настройка даты и времени  
  * Localisation Options
  * Change Timezone
    * Europe
    * Riga

<a id="chapter-2"></a>  

## Установка нужных пакетов  
Перед установкой нужно выполнить 2 команды  
```
sudo apt-get upgrade  
sudo apt-get update
```

* Для работы с ssh `sudo apt-get install ssh`  
* Для даты и времени `sudo apt-get install ntp`  
* Для работы lbrcmEGL и lbrcmGLESv2 `sudo apt-get install libglfw3-dev libgles2-mesa-dev`  
* Клиент и демон ftp `sudo apt-get install ftp ftpd`  
* Для работы с openVG `sudo apt-get install libjpeg8-dev indent libfreetype6-dev ttf-dejavu-core`  
* Для работы с png `libpng-dev`  
* Для работы с cURL `sudo apt-get install libcurl4-openssl-dev`  
* Установка Git `sudo apt-get install git`  
* Установка Midnight commander `sudo apt-get install mc`  

<a id="chapter-3"></a> 

## Установка и проверка openVG  
```
git clone https://github.com/ajstarks/openvg  
cd openvg  
```
> Изменяем **Makefile** -> `sudo nano Makefile`  
> В переменной LIBFLAGS  
> -lEGL -lGLESv2 меняем на -lbrcmEGL -lbrcmGLESv2  
```
make  
sudo make install  
cd client  
```
> Изменяем **Makefile** -> `sudo nano Makefile`  
> В переменной LIBFLAGS  
> -lEGL -lGLESv2 меняем на -lbrcmEGL -lbrcmGLESv2  

`make test`  
Запускаем тест -> `./shapedemo`
*Для немедленного выхода из запущенной программы* горячая клавиша -> `Ctrl + C`  

<a id="chapter-4"></a> 

## Настройка статичного ip
Если делать изменения в `/etc/netwrok/interfaces` то *dchl* может блокировать нужные настройки и выдовать динамический ip.  
Поэтому изменения делаем в `/etc/dhcpcd.conf`  

(прописываем нужные нам адреса)  
```
interface eth0  
static ip_address=192.168.0.100/24  
static routers=192.168.0.1  
static domain_name_servers=192.168.0.300 8.8.8.8  
```