University: [ITMO University](https://itmo.ru/ru/)  
Faculty: [FICT](https://fict.itmo.ru)  
Course: [IP-telephony](https://github.com/itmo-ict-faculty/ip-telephony)  
Year: 2023/2024  
Group: K34202  
Author: Gladusko Olga  
Lab: Lab2  
Date of create: 22.02.2024  
Date of finished: .02.2024  

---
# Отчет по лабораторной работе №2  
## "Конфигурация voip в среде Сisco packet tracer"  

### Цель работы  
Изучить построение сети IP-телефонии с помощью маршрутизатора Cisco 2811, коммутатора Cisco catalyst 3560 и IP телефонов Cisco 7960.  

## Ход работы  
### Часть 1
В Сisco packet tracer была собрана схема с роутером, коммутатором и 3 телефонами:  
![.](https://github.com/OlgaGladushko/2023_2024-ip-telephony-k34202-gladushko_o/blob/main/lab2/imgs/topo1.jpg)  
В конфигурационном режиме было изменено название маршрутизатора на CMERouter командой ```hostname CMERouter```.  
Синтаксис ввода слов от DNS серверов был отключен командой ```hostname CMERouter```.  
Для защиты маршрутизатора в удаленном режиме (для 5 виртуальных консолей) и в режиме консоли были заданы пароли командами:  
```
line vty 0 4
password 123
login
exit
lie console 0
password 123
login
```
Далее был настрен интерфейс fa0/0 на маршрутизаторе: выдан IP-адрес и маска, переведен в режим On. Также был настроен DHCP пул с указанием сети и выданного роутеру адреса 192.168.0.1 командами, и задана опция 150 для работы IP-телефонии командами:  
```
ip dhcp pool voice
network 192.168.0.0 255.255.255.0
default-router 192.168.0.1
option 150 ip 192.168.0.1
```
На роутере также был создан сервис IP-телефонии, вмещающий 10 устройств, порт маршрутизатора и количество линий командами:  
```
max-dn 10
max-ephones 10
ip source-address 192.168.0.1 port 3100
auto assign 1 to 19
```  
Далее был создан VLAN на коммутаторе для всех занятых портов командами:  
```
interface range fa0/1-4
switchport mode access
switchport voice vlan 1
```
На роутере была продолжена настройка телефонии, были выданы номера 001, 002 и 003 командами:  
```
ephone-dn 1
number 001
exit
ephone-dn 2
number 002
exit
ephone-dn 3
number 003
```  
Телефоны были подключены к блоку питания в окне физического представления. Работоспособность была проверена путем звонка, также в физическом представлении был введен номер другого телефона:  
![.](https://github.com/OlgaGladushko/2023_2024-ip-telephony-k34202-gladushko_o/blob/main/lab2/imgs/call1.jpg)  
Как видно, соединение было установлено, на экранах виднен номер телефона, с которым установлена связь.  

