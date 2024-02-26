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
тип friend (для совершения и принятия вызвов), разрешение подключения с разных IP-адресов, пароль и имя контекста  
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
