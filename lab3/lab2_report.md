University: [ITMO University](https://itmo.ru/ru/)  
Faculty: [FICT](https://fict.itmo.ru)  
Course: [IP-telephony](https://github.com/itmo-ict-faculty/ip-telephony)  
Year: 2023/2024  
Group: K34202  
Author: Gladusko Olga  
Lab: Lab3  
Date of create: 26.02.2024  
Date of finished: 27.02.2024  

---
# Отчет по лабораторной работе №3  
## "Использование Asterisk в качестве SIP proxy"  

### Цель работы  
Изучить программный комплекс Asterisk. Настройка Asterisk для локальных звонков.  

## Ход работы 
На Ubuntu был установлен Asterisk командой ```sudo apt-get install asterisk```.  
Далее в директории /etc/asterisk был открыт файл sip.conf, куда была добавлена информация о телефонах 1000 и 1001: 
тип friend (для совершения и принятия вызовов), разрешение подключения с разных IP-адресов, пароль и имя контекста  
```
[1000]
type=friend
host=dynamic
secret=123
context=ext_1000

[1001]
type=friend
host=dynamic
secret=123
context=ext_1001
```  
В файл extensions.conf были определены екстеншены в указанных ранее контекстах: 
вызов должен осуществляться по введенному номеру, тип канала – SIP  
```
[ext_1000]
exten => _XXXX,1,Dial(SIP/${EXTEN})

[ext_1001]
exten => _XXXX,1,Dial(SIP/${EXTEN})
```  
После измененя файлов Asterisk был перезапущен для вступления в силу изменений командой 
```sudo service asterisk restart```. Статус сервиса был проверен, как видно он был успешно запущен:  
![.](https://github.com/OlgaGladushko/2023_2024-ip-telephony-k34202-gladushko_o/blob/main/lab3/imgs/status.jpg)  
Далее были установлены софтфоны Zoiper5 и MicroSIP. Так работа выполнялась на Ubuntu нужно было также установить wine, настроить и с помощью него уже установить MicroSIP.  
Далее софтфоны были подключены: введены указанные ранее номера и пароли, а также адрес сервера – адрес текущего хоста 127.0.0.1.  
Настройка Zoiper5:  
![.](https://github.com/OlgaGladushko/2023_2024-ip-telephony-k34202-gladushko_o/blob/main/lab3/imgs/Zoiper5.jpg)  
Настройка MicroSIP:  
![.](https://github.com/OlgaGladushko/2023_2024-ip-telephony-k34202-gladushko_o/blob/main/lab3/imgs/MicroSIP.jpg)  
Для проврки успешной настройки связи был совершен звонок на телефон 1000 с телефона 1001. Как видно, соединение было установлено, на экране виден номер звонящего телефона:  
![.](https://github.com/OlgaGladushko/2023_2024-ip-telephony-k34202-gladushko_o/blob/main/lab3/imgs/call.jpg)  

### Вывод  
В ходе лабораторной работы был настроен Asterisk для локальных звонков, в результате чего успешно установлена связь между софтфонами.
