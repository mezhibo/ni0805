**Задание 1**

На схеме представлена топология сети офиса:

![Image alt](https://github.com/mezhibo/ni0805/blob/3bd5334ccf56a05f72a3f3eb3d28e662faabca53/IMG/1.jpg)


На офисном МЭ - CiscoASA есть 5 интерфейсов, 4 для сегментации локальной сети и 1 публичная сеть (Outside):

 - Inside - Gi0/1 - Vlan 10 - 192.168.10.1/24

 - Backup - Gi0/2 - Vlan 20 - 192.168.20.1/24

 - DMZ - Gi0/3 - Vlan 30 - 192.168.30.1/24

 - Monitoring - Gi1/0 - Vlan 40 - 192.168.40.1/24

 - Outside- Gi0/0 - vlan 50 - 100.100.100.1/24


Необходимо создать зоны с уровнями безопасности (security-level) следующим образом:

1. Из Inside можно подключаться ко всем сетям.

2. Из Backup можно подключаться ко всем, кроме Inside.

3. Из Monitoring можно подключаться только к DMZ и Outside.

4. Из DMZ можно подключаться только к Outside.


Каким образом надо назначить уровни безопасности на интерфейсы Cisco ASA?



**Решение 1**


Для получения требуемого результата на соответствующих интефейсах настраиваются следующие значения security-level:

```
interface Gi0/1
 nameif Inside
 security-level 100
 ip address 192.168.10.1 255.255.255.0

interface Gi0/2
 nameif Backup
 security-level 90
 ip address 192.168.20.1 255.255.255.0

interface Gi1/0
 nameif Monitoring
 security-level 80
 ip address 192.168.40.1 255.255.255.0

interface Gi0/3
 nameif DMZ
 security-level 70
 ip address 192.168.30.1 255.255.255.0

interface Gi0/0
 nameif Outside
 security-level 0
 ip address 100.100.100.1 255.255.255.0
```
