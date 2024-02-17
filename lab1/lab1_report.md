University: [ITMO University](https://itmo.ru/ru/)  
Faculty: [FICT](https://fict.itmo.ru)  
Course: [IP-telephony](https://github.com/itmo-ict-faculty/ip-telephony)  
Year: 2023/2024  
Group: K34202  
Author: Gladusko Olga  
Lab: Lab1  
Date of create: 17.02.2024  
Date of finished: .02.2024  

---
# Отчет по лабораторной работе №1  
## "Базовая настройка ip-телефонов в среде Сisco packet tracer"  

### Цель работы  
Изучить рабочую среду Cisco Packet Tracer, ознакомиться с интерфейсами основных устройств, типами кабелей, научиться собирать топологию. Изучить построение сети IP-телефонии с помощью маршрутизатора, коммутатора и IP телефонов Cisco 7960 в среде Packet tracer  

## Ход работы  
### Часть 1
В Сisco packet tracer была собрана схема соединения 4 коммутаторов и 7 ПК:  
![.](https://github.com/OlgaGladushko/2022_2023-ip-telephony-k34202-gladushko_o/blob/main/lab1/imgs/topo1.jpg)  
Всем ПК были назначены адреса из подсети 192.168.10.0/24:  
![.](https://github.com/OlgaGladushko/2022_2023-ip-telephony-k34202-gladushko_o/blob/main/lab1/imgs/pc_address.jpg)  
Для связи всех ПК не было необходимости дополнительной настройки коммутатора, так как все порты были подняты автоматически. Связь была проверена пингами с ПК, подключенных к разным коммутаторам:  
![.](https://github.com/OlgaGladushko/2022_2023-ip-telephony-k34202-gladushko_o/blob/main/lab1/imgs/ping_pc1.jpg)  
![.](https://github.com/OlgaGladushko/2022_2023-ip-telephony-k34202-gladushko_o/blob/main/lab1/imgs/ping_pc2.jpg)  
Как видно, все пинги прошли успешно.

### Часть 2
Далее была собрана схема соединения с роутером, коммутатором и двумя IP-телефонами:  
![.](https://github.com/OlgaGladushko/2022_2023-ip-telephony-k34202-gladushko_o/blob/main/lab1/imgs/topo2.jpg)  
Было изменено имя маршрутизатора командой ```hostname CMERouter```.  
Также был настроен интерфейс, идущий на коммутатор: включен и назначен адрес 192.168.0.1/24.  
Далее был создан пул адресов для телефонов из подсети 192.168.0.0/24, был указан адрес маршрутизатора и задана опция 150 для работы IP-телефонии командами:  
```
ip dhcp pool phones
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
На коммутаторе была включена поддержка VoIP-интерфейсов:  
```
interface range FastEthernet 0/1 - FastEthernet 0/3
switchport mode access
sitchport voice vlan 1
```  
На роутере была продолжена настройка телефонии, были выданы номера 001 и 002 командой:  
```
ephone-dn 1
number 001
exit
ephone-dn 2
number 002
```  
Телефоны были подключены к блоку питания в окне физического представления:  
![.](https://github.com/OlgaGladushko/2022_2023-ip-telephony-k34202-gladushko_o/blob/main/lab1/imgs/phone.jpg)  
Работоспособность была проверена путем звонка, также в физическом представлении был введен номер другого телефона:  
![.](https://github.com/OlgaGladushko/2022_2023-ip-telephony-k34202-gladushko_o/blob/main/lab1/imgs/call.jpg)  
Как видно, соединение было установлено, на экранах видны номера телефона, с которым установлена связь.  
### Вывод  
В ходе лабораторной работы были собраны представленные схемы связи, настроены устройства, в результате чего успешно установлена связь между ПК в первой части, и между IP-телефонами – во второй.
