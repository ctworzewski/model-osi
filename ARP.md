# ARP

## Windows

* `arp -a` - wyświetla tablicę ARP
* arp -d
* arp -d *

* arp -s 192.168.3.4 00-66-77-88-ee - ten mac jest tymczasowo/ po wyłączeniu kompa usunie się z pamięci RAM
albo 
* netsh interface ipv4 add neighbor "local area connection" 10.1.1.1 aa-bb-cc-dd-ee-ff - ten wpis jest na stałe z tym mac
* netsh interface ipv4 dell neighbor "local area connection" 10.1.1.1

* lekcja 14, 2:23:00

przypisać ip i wymyslony mac, potem pingnac i nie będzie działać, a potem wprowadizć poprawny
