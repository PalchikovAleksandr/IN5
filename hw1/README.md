> 1) Запишите адрес сети 10.255.3.0/24 вместе с маской в виде четырех последовательностей из восьми бит, разделенных точками (маска сети так же должна быть записана последовательностями бит). Для этой сети запишите в виде четырех последовательностей из восьми бит, разделенных точками, минимальное и максимальное значение адреса хоста в сети.

00001010.11111111.00000011.00000000 (10.255.3.0)  
11111111.11111111.11111111.00000000 (255.255.255.0)
  
00001010.11111111.00000011.00000001 (min 10.255.3.1)  
00001010.11111111.00000011.11111110 (max 10.255.3.254)

> 2) Что из нижеперечисленного является адресом хоста, а что адресом сети?  
> 10.255.0.13  
192.168.1.0/23  
192.168.333.1  
173.25.16.0/28  
87.245.219.8/29  
192.168.0.3/32  
127.0.0.1  
10.1.14.7/24

10.255.0.13 - адрес хоста  
192.168.1.0/23 - адрес сети  
192.168.**333**.1  - ошибка  
173.25.16.0/28 - адрес сети  
87.245.219.8/29 - адрес сети  
192.168.0.3/32 - адрес хоста  
127.0.0.1 - адрес хоста с которого обращаются/самого себя   
10.1.14.7/24 - адрес сети  

> 3) Какие из нижеперечисленных IP-адресов являются адресами локальной сети, а какие - глобальной?  
10.255.0.13  
8.8.8.8  
10.0.0.254  
194.12.53.5  
109.73.40.164  
172.33.1.3  

10.255.0.13 - локалный  
8.8.8.8 - глобальный  
10.0.0.254 - локалный  
194.12.53.5 - глобальный  
109.73.40.164 - глобальный  
172.33.1.3  - локалный  

> 4) Какой из порядков инкапсуляции протоколов верный (направление от клиентского приложения к началу передачи по каналу связи)?  
>- http-пакет - ip-пакет - tcp-сегмент - ethernet-фрейм - физический сигнал
>- физический сигнал - ethernet-фрейм - ip-пакет - tcp-сегмент - http-пакет
>- tcp-сегмент - http-пакет - ip-пакет - ethernet-фрейм - физический сигнал - верный
>- http-пакет - tcp-сегмент - ip-пакет - ethernet-фрейм - физический сигнал
>- ethernet-фрейм - http-пакет - tcp-сегмент - ip-пакет - физический сигнал  

ethernet-фрейм - http-пакет - tcp-сегмент - ip-пакет - физический сигнал - верный

> 5) Определите внешний IP-адрес, под которым вы выходите в сеть Интернет.
```
shurik@fedora:~$  curl -s http://whatismijnip.nl |cut -d " " -f 5  
```
**213.251.255.37**

> 6) Определите MAC-адреса сетевой карты вашего компьютера/ноутбука (если их несколько, то почему?) и WI-FI интерфейса смартфона.

```
shurik@fedora:~$ ifconfig
```
Сетевушка Вафли c маком 6c:4b:90:60:18:42:  
> enp0s31f6: flags=4163<UP,BROADCAST,RUNNING,MULTICAST>  mtu 1500  
inet 192.168.13.6  netmask 255.255.255.0  broadcast 192.168.13.255  
inet6 fe80::cc61:892b:f842:e882  prefixlen 64  scopeid 0x20<link>  
ether ***6c:4b:90:60:18:42***  txqueuelen 1000  (Ethernet)  
RX packets 482698  bytes 486548112 (464.0 MiB)  
RX errors 0  dropped 0  overruns 0  frame 0  
TX packets 337989  bytes 79406038 (75.7 MiB)  
TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0  
device interrupt 17  memory 0xf7200000-f7220000  

Сейчас на стационарном, тут 1 сетевушка, на ноуте было бы 2, вафля и блюпуп.

![](https://cloud.palchikov.name/photo_2024-09-23_17-27-40.jpg "18:69:D4:AF:BB:FF")



> 7) Определите IP-адрес вашего компьютера/ноутбука в локальной сети и маску сети.  

```
shurik@fedora:~$ ifconfig
```
IP: 192.168.13.6/24 (255.255.255.0)
> enp0s31f6: flags=4163<UP,BROADCAST,RUNNING,MULTICAST>  mtu 1500  
inet ***192.168.13.6***  netmask ***255.255.255.0***  broadcast 192.168.13.255  
inet6 fe80::cc61:892b:f842:e882  prefixlen 64  scopeid 0x20<link>  
ether 6c:4b:90:60:18:42  txqueuelen 1000  (Ethernet)  
RX packets 482698  bytes 486548112 (464.0 MiB)  
RX errors 0  dropped 0  overruns 0  frame 0  
TX packets 337989  bytes 79406038 (75.7 MiB)  
TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0  
device interrupt 17  memory 0xf7200000-f7220000  

> 8) Определите IP-адрес шлюза по умолчанию (default gateway) для вашего компьютера/ ноутбука.    

```
shurik@fedora:~$ ip route | grep default
```
> default via **192.168.13.1** dev enp0s31f6 proto dhcp src 192.168.13.6 metric 100 

> 9) Просканируйте утилитой nmap шлюз по умолчанию вашего компьютера, какие порты на каких протоколах транспортного уровня на нем открыты?
```
shurik@fedora:~$ nmap 192.168.13.1
```
> Starting Nmap 7.92 ( https://nmap.org ) at 2024-09-23 17:44 MSK  
Nmap scan report for _gateway (192.168.13.1)  
Host is up (0.0047s latency).  
Not shown: 997 closed tcp ports (conn-refused)  
PORT    STATE SERVICE  
53/tcp  open  domain  
80/tcp  open  http  
443/tcp open  https  
Nmap done: 1 IP address (1 host up) scanned in 0.42 seconds  

Открыты:  
**53 - tcp    
80 - tcp  
443 - tcp**


> 10) Просканируйте утилитой nmap хосты m.ompk.ru, edu.russeas.ru, 194.12.56.27, какие порты на каких протоколах транспортного уровня на них открыты?  

```
shurik@fedora:~$ nmap m.ompk.ru
```
> Starting Nmap 7.92 ( https://nmap.org ) at 2024-09-23 17:53 MSK  
Nmap scan report for m.ompk.ru (178.248.234.188)  
Host is up (0.020s latency).  
Not shown: 998 filtered tcp ports (no-response)  
PORT    STATE SERVICE  
80/tcp  open  http  
443/tcp open  https  
Nmap done: 1 IP address (1 host up) scanned in 6.35 seconds  

Открыты:  
80 - tcp  
443 - tcp  

```
shurik@fedora:~$ nmap edu.russeas.ru
```
> Starting Nmap 7.92 ( https://nmap.org ) at 2024-09-23 17:56 MSK  
Nmap scan report for edu.russeas.ru (194.12.56.22)  
Host is up (0.020s latency).  
Not shown: 988 filtered tcp ports (no-response), 9 filtered tcp ports (host-unreach)  
PORT    STATE SERVICE  
22/tcp  open  ssh  
80/tcp  open  http  
443/tcp open  https  
Nmap done: 1 IP address (1 host up) scanned in 4.76 seconds  


22 - tcp - ssh  
80 - tcp - www без ssl  
443 - tcp - www c ssl  

```
shurik@fedora:~$ nmap 194.12.56.27
```
> Starting Nmap 7.92 ( https://nmap.org ) at 2024-09-23 18:01 MSK  
Nmap scan report for mail.complex-systems.biz (194.12.56.27)  
Host is up (0.030s latency).  
Not shown: 978 filtered tcp ports (no-response), 17 filtered tcp ports (host-unreach)  
PORT    STATE SERVICE  
22/tcp  open  ssh  
25/tcp  open  smtp  
80/tcp  open  http  
465/tcp open  smtps  
993/tcp open  imaps  
 



> 11) Выведите таблицу маршрутизации вашего компьютера. По какому из маршрутов пойдет трафик к:  
шлюзу по умолчанию (192.168.13.1)  
хосту 8.8.8.8  
хосту 10.1.1.1  
Ко всем ли хостам из списка трафик дойдет успешно? Почему?
  
```
shurik@fedora:~$ ip route  
```
> default via 192.168.13.1 dev enp0s31f6 proto dhcp src 192.168.13.6 metric 100   
192.168.13.0/24 dev enp0s31f6 proto kernel scope link src 192.168.13.6 metric 100   

Правил нет, весь трафик будет проходить череш шлюз

```
shurik@fedora:~$ traceroute 8.8.8.8
```
traceroute to 8.8.8.8 (8.8.8.8), 30 hops max, 60 byte packets  
 1  _gateway (192.168.13.1)  0.489 ms  0.505 ms  0.484 ms  
 2  192.168.91.1 (192.168.91.1)  32.348 ms  32.566 ms  32.533 ms  
 3  3031.GE0-9.bone-01.tm.countrycom.ru (213.251.255.33)  3.808 ms  33.605 ms  4.578 ms  
 4  213.251.208.156 (213.251.208.156)  4.826 ms  4.795 ms  5.130 ms  
 5  msk-ix-gw3.google.com (195.208.208.250)  5.904 ms  5.873 ms  5.395 ms  
 6  * * 192.178.241.251 (192.178.241.251)  26.183 ms  
 7  * 192.178.241.234 (192.178.241.234)  6.433 ms 192.178.241.70 (192.178.241.70)  25.248 ms  
 8  142.250.238.138 (142.250.238.138)  18.301 ms * 209.85.249.158 (209.85.249.158)  19.854 ms  
 9  172.253.65.82 (172.253.65.82)  45.530 ms  31.367 ms 142.250.235.68 (142.250.235.68)  40.774 ms  
10  216.239.42.23 (216.239.42.23)  21.689 ms 216.239.56.101 (216.239.56.101)  39.783 ms 172.253.64.51 (172.253.64.51)  40.882 ms  
11  * * *  
*  
19  * * *  
20  dns.google (8.8.8.8)  31.349 ms  31.550 ms  30.951 ms  
```
shurik@fedora:~$ traceroute 10.1.1.1
```  
traceroute to 10.1.1.1 (10.1.1.1), 30 hops max, 60 byte packets  
1  _gateway (192.168.13.1)  1.056 ms  0.984 ms  0.360 ms  
2  192.168.91.1 (192.168.91.1)  1.191 ms  1.137 ms  1.142 ms  
3  3031.GE0-9.bone-01.tm.countrycom.ru (213.251.255.33)  2.444 ms  2.203 ms  2.497 ms  
4  213.251.208.156 (213.251.208.156)  2.444 ms  2.662 ms  2.025 ms  
5  * * *  
*  
30  * * *

Я нахожучь в локальной сети 192.168.13.0/24 не в 10.1.1.0/24 трафик потеряется и никуда не придет. До всех отсальных адресов проблем не будет.
