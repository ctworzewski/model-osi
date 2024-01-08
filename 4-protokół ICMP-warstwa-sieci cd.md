# protokół ICMP
* Protokół ICMP to protokoół kontrolno diagnostyczny...

  Ciekawa anegdota:
![Alt text](https://i.ibb.co/NFk0hWb/icmp.png "ICMP")

Załóżmy, że komputer `1A` wysyła, żądanie do serwera `Serwer Eagle`, aby ten otworzył mu stronę www, żadanie to idzie przez `switch` oraz `dwa routery`.
Połączenie dochodzi do tego `Eagle` ale on mówi, że nie ma `serwera www` i co teraz???
Dobrze byłoby, gdyby `Serweer Eagle` powiedział komputerowi `1A`, że on nie ma takiego serwera.

Ogólnie, problem może być taki, że coś nie działa po drodze:
* firewall
* uszkodzony kabel na hoście źrodłowym lub końcowym,
* problem z ktorymś z routerów po drodze lub switch

* Komunikat ICMP to jest list, któy jest w sumie dość dziwny, jest to protokół warstwy trzeciej, to ciekawie to wygląda, że my tj. tworzymy list, któy nie jest wiadomością z poziomu warstwy aplikacji, tyko list utworzony w ramach warstwty sieci i  zapakowany w pakiet IP, więc w kopertę, ale to będzie list w podwójna koperata, nie potrójnej - bo tu nie ma TCP ani UDP.
To co tutaj jest, kest wsadzane do pakietu IP. A pakiet IP będzie pakowany jeszcze w `ramkę Ethnernetową` pakowany - dlatego podwójna koperta.
* na tym liście jest dziwnie, bo tutaj są tak jakby tylko dwa pola to  `Type` oraz `Code` - tam są wysyłane tylko liczby. Ajakie są to liczby??? O takie:
  ![Alt text](https://i.ibb.co/brnjLxX/icmp2.png "ICMP")

  
