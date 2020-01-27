# Настройка MPLS

Смотреть схему MPLS.png

Для организации сетевой доступности (IP) будем использовать протокол динамической маршрутизации OSPF.
Настроим роутер Router15:
* Заходим в режим конфигурации роутера
```
Router15#conf t
```
* Включаем Cisco Express Forwarding, технология быстрой коммутации пакетов на 3-ем уровне компании cisco (если не включено)
```
Router15(config)#ip cef 
```
* Включаем глобально процесс коммутации по меткам (MPLS);
```
Router15(config)#mpls ip 
```
* Выбираем протокол, по которому будут обмениваться метками LSR (ELSR) между собой (есть еще TDP, он является проприетарным);
```
Router15(config)#mpls label protocol ldp 
```
* Определяем, какой интерфейс (IP-адрес) берется в качестве ID роутера в процессе MPLS;
```
Router15(config)#mpls ldp router-id loopback 0
```
* Настраиваем интерфейсы и включаем mpls
```
Router15(config)#int e0/0
Router15(config-if)#mpls ip 
Router15(config)#exit
Router15(config)#int e0/1
Router15(config-if)#mpls ip 
```
Настроим подобным образом остальные роутеры.
```
Router14#conf t
Router14(config)#ip cef 
Router14(config)#mpls ip 
Router14(config)#mpls label protocol ldp 
Router14(config)#mpls ldp router-id loopback 0
Router14(config)#int e0/0
Router14(config-if)#mpls ip 
Router14(config)#exit
Router14(config)#int e0/1
Router14(config-if)#mpls ip 
Router14(config)#exit
Router14(config)#int e0/2
Router14(config-if)#mpls ip 


Router16#conf t
Router16(config)#ip cef 
Router16(config)#mpls ip 
Router16(config)#mpls label protocol ldp 
Router16(config)#mpls ldp router-id loopback 0
Router16(config)#int e0/0
Router16(config-if)#mpls ip 
Router16(config)#exit
Router16(config)#int e0/1
Router16(config-if)#mpls ip 


Router17#conf t
Router17(config)#ip cef 
Router17(config)#mpls ip 
Router17(config)#mpls label protocol ldp 
Router17(config)#mpls ldp router-id loopback 0
Router17(config)#int e0/0
Router17(config-if)#mpls ip 
Router16(config)#exit
Router17(config)#int e0/1
Router17(config-if)#mpls ip 
Router16(config)#exit
Router17(config)#int e0/2
Router17(config-if)#mpls ip 
Router17(config)#exit
```
Проверку осуществим с помощью команды show :
```
Sh mpls forwarding-table
```
В результате появится таблица с метками.


