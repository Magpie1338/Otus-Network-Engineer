# Лабораторная работа 002

## Задание:
### 1. Настройка DHCP v.4 
1. 1. Создание сети и настройка основных параметров устройства
1. 2. Настройка и проверка DHCP v.4 на маршрутизатора R1
1. 3. Настройка и проверка DHCP Relay на маршрутизаторе R2

## Таблица адресации
|Устройство    |Интрефейс       |IP-адрес    |Маска подсети   |
| ------------ | ------------ | ------------ |----------------|
|  s1          | VLAN 1       | 192.168.1.1  | 255.255.255.0  |
|  s2          | VLAN 1       | 192.168.1.2  | 255.255.255.0  |
|  s3          | VLAN 1       | 192.168.1.3  | 255.255.255.0  |


## 1. Схема лабораторной работы 
![](schema-lab003-DHCPv4.jpg)

## 2. Выбор корневого моста
### Коммутатор s1
<pre>
s1#show spanning-tree

VLAN0001
  Spanning tree enabled protocol rstp
  Root ID    Priority    32769
             Address     5000.0001.0000
             This bridge is the root
             Hello Time   2 sec  Max Age 20 sec  Forward Delay 15 sec

  Bridge ID  Priority    32769  (priority 32768 sys-id-ext 1)
             Address     5000.0001.0000
             Hello Time   2 sec  Max Age 20 sec  Forward Delay 15 sec
             Aging Time  300 sec

Interface           Role Sts Cost      Prio.Nbr Type
------------------- ---- --- --------- -------- --------------------------------
Gi0/0               Desg FWD 4         128.1    Shr
Gi0/2               Desg FWD 4         128.3    Shr
</pre>

### Коммутатор s2
<pre>
s2#show spanning-tree

VLAN0001
  Spanning tree enabled protocol rstp
  Root ID    Priority    32769
             Address     5000.0001.0000
             Cost        4
             Port        1 (GigabitEthernet0/0)
             Hello Time   2 sec  Max Age 20 sec  Forward Delay 15 sec

  Bridge ID  Priority    32769  (priority 32768 sys-id-ext 1)
             Address     5000.0002.0000
             Hello Time   2 sec  Max Age 20 sec  Forward Delay 15 sec
             Aging Time  300 sec

Interface           Role Sts Cost      Prio.Nbr Type
------------------- ---- --- --------- -------- --------------------------------
Gi0/0               Root FWD 4         128.1    Shr
Gi1/0               Desg FWD 4         128.5    Shr
</pre>
### Коммутатор s3
<pre>
s3#show spanning-tree

VLAN0001
  Spanning tree enabled protocol rstp
  Root ID    Priority    32769
             Address     5000.0001.0000
             Cost        4
             Port        3 (GigabitEthernet0/2)
             Hello Time   2 sec  Max Age 20 sec  Forward Delay 15 sec

  Bridge ID  Priority    32769  (priority 32768 sys-id-ext 1)
             Address     5000.0003.0000
             Hello Time   2 sec  Max Age 20 sec  Forward Delay 15 sec
             Aging Time  300 sec

Interface           Role Sts Cost      Prio.Nbr Type
------------------- ---- --- --------- -------- --------------------------------
Gi0/2               Root FWD 4         128.3    Shr
Gi1/0               Altn BLK 4         128.5    Shr
</pre>
</b>Коммутатор s1 является корневым.</b>

Коммутатор s1 MAC:5000.0001.0000
Gi0/0 - Designated port
Gi0/2 - Designated port

Коммутатор s2 MAC:5000.0002.0000
Gi0/0 - Root port
Gi1/0 - Designated port

Коммутатор s3 MAC:5000.0003.0000
Gi0/2 - Root port 
Gi1/0 - Alternative port



## 3. Изменение протокола Spanning-tree при изменении стоимости порта

### На коммутаторе s3 (коммутатор с заблокированным портом) на порту Gi0/2 меняем стоимость
<pre>
s3#show spanning-tree

VLAN0001
  Spanning tree enabled protocol rstp
  Root ID    Priority    32769
             Address     5000.0001.0000
             Cost        8
             Port        5 (GigabitEthernet1/0)
             Hello Time   2 sec  Max Age 20 sec  Forward Delay 15 sec

  Bridge ID  Priority    32769  (priority 32768 sys-id-ext 1)
             Address     5000.0003.0000
             Hello Time   2 sec  Max Age 20 sec  Forward Delay 15 sec
             Aging Time  300 sec

Interface           Role Sts Cost      Prio.Nbr Type
------------------- ---- --- --------- -------- --------------------------------
Gi0/2               Altn BLK 30        128.3    Shr
Gi1/0               Root FWD 4         128.5    Shr
</pre>

В результате интерфейс Gi1/0 стал Root портом, а интерфейс Gi0/2 стал альтернативным портом.

## Выбор протоколом STP порта исходя из приорите портов
### Коммутатор s1
<pre>
s1#show spanning-tree

VLAN0001
  Spanning tree enabled protocol rstp 
   Root ID    Priority    32769  
             Address     5000.0001.0000
             This bridge is the root
             Hello Time   2 sec  Max Age 20 sec  Forward Delay 15 sec

  Bridge ID  Priority    32769  (priority 32768 sys-id-ext 1)
             Address     5000.0001.0000
             Hello Time   2 sec  Max Age 20 sec  Forward Delay 15 sec
             Aging Time  300 sec

Interface           Role Sts Cost      Prio.Nbr Type
------------------- ---- --- --------- -------- --------------------------------
Gi0/0               Desg FWD 4         128.1    Shr
Gi0/1               Desg FWD 4         128.2    Shr
Gi0/2               Desg FWD 4         128.3    Shr
Gi0/3               Desg FWD 4         128.4    Shr

</pre>

### Коммутатор s2
<pre>
s2#show spanning-tree

VLAN0001
  Spanning tree enabled protocol rstp
  Root ID    Priority    32769
             Address     5000.0001.0000
             Cost        4
             Port        1 (GigabitEthernet0/0)
             Hello Time   2 sec  Max Age 20 sec  Forward Delay 15 sec

  Bridge ID  Priority    32769  (priority 32768 sys-id-ext 1)
             Address     5000.0002.0000
             Hello Time   2 sec  Max Age 20 sec  Forward Delay 15 sec
             Aging Time  300 sec

Interface           Role Sts Cost      Prio.Nbr Type
------------------- ---- --- --------- -------- --------------------------------
Gi0/0               Root FWD 4         128.1    Shr
Gi0/1               Altn BLK 4         128.2    Shr
Gi1/0               Desg FWD 4         128.5    Shr
Gi1/1               Desg FWD 4         128.6    Shr
   

</pre>
### Коммутатор s3
<pre>
s3#show spanning-tree

VLAN0001
  Spanning tree enabled protocol rstp
  Root ID    Priority    32769
             Address     5000.0001.0000
             Cost        4
             Port        3 (GigabitEthernet0/2)
             Hello Time   2 sec  Max Age 20 sec  Forward Delay 15 sec

  Bridge ID  Priority    32769  (priority 32768 sys-id-ext 1)
             Address     5000.0003.0000
             Hello Time   2 sec  Max Age 20 sec  Forward Delay 15 sec
             Aging Time  300 sec

Interface           Role Sts Cost      Prio.Nbr Type
------------------- ---- --- --------- -------- --------------------------------
Gi0/2               Root FWD 4         128.3    Shr
Gi0/3               Altn BLK 4         128.4    Shr
Gi1/0               Altn BLK 4         128.5    Shr
Gi1/1               Altn BLK 4         128.6    Shr
</pre>
</b>Коммутатор s1 является корневым.</b>

Коммутатор s1 MAC:5000.0001.0000
Gi0/0 - Designated port
Gi0/1 - Designated port
Gi0/2 - Designated port
Gi0/3 - Designated port

Коммутатор s2 MAC:5000.0002.0000
Gi0/0 - Root port
Gi0/1 - Alternative port
Gi1/0 - Designated port
Gi1/1 - Designated port

Коммутатор s3 MAC:5000.0003.0000
Gi0/2 - Root port 
Gi0/3 - Alternative port 
Gi1/0 - Alternative port
Gi1/1 - Alternative port
