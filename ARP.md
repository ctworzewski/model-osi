# ARP

## Windows

* `arp -a` - wyświetla tablicę ARP
* arp -d
* arp -d *

* arp -s 192.168.3.4 00-66-77-88-ee
albo 
* netsh interface ipv4 add neighbor "local area connection" 10.1.1.1 aa-bb-cc-dd-ee-ff

przypisać ip i wymyslony mac, potem pingnac i nie będzie działać, a potem wprowadizć poprawny
