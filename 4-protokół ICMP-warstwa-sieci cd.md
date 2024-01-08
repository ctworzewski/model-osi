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
* na tym liście jest dziwnie, bo tutaj są tak jakby tylko dwa pola to  `Type` oraz `Code` - tam są wysyłane tylko liczby. A jakie są to liczby w praktyce??? O takie:
  
  ![Alt text](https://i.ibb.co/brnjLxX/icmp2.png "ICMP")

  Pole typ może być `0`, to jest `Echo Replay`.
  Jeśli wysyłamy `ping wp.pl`, to w polu typ wstawia się `8`

## TTL (Time-to-Live)
TTL to tzw. `czas życia pakietu`.
W sieci Internet istnieje taki problem, nazywany `pętlą routingu`, czyli, że pakiet, który został wysłany, może krązyć w nieskonczoność, pomiędzy roujterami, po prostu się zgubi.
Jeśli nic nie zrobimy z takim pakietem to kwestia czasu, kiedy się Internet wypełni od takich pakietów i po prostu padnie Internet na całym świecie.

Więc wymyślono coś, żeby przeciwdziaąlć takim sytuacją i właśnie jednym ze sposobów jest `Pole TTL`, które ma m.in. zapobiegać powstawaniu pętlą routingu.

Jeśli mój komputer w tym momencie generuje jakiś pakiet IP i chce go wysłać w sieć, to domyslnie w polu TTL wstawia liczbę pomiędzy  0-255.
Widząc dany TTL, często można zobaczyć, z jakiego systemu operacyjnego zostąło coś wysłane.
Każdy system wstawia inną liczbę np:
* Windows: TTL=128
* Linux: TTL=64

### Jak to dziaa, to jest istotne?
Założmy, że wysyłamy pakiet z wartością początkową TTL=128, co się dzieje dalej... jeśli przechodzi ten pakiet przez router, to router w tym momencie ma obowiązek pomniejszyć to pole TTL o 1 przed wypuszczeniem tego pakietu dalej.
Po zrealizowaniu procesu routingu ale przed wypuszczeniem dalej pakietu IP musi pomniejszyć o jeden. Jeśli router dostanie pakiet, gdzie jest ustawione pole TTL=1 to on teraz pomniejsza to o 1, i TTL=0. Jesli jest 0, to teraz on musi wyrzucić to do kosza i nie może przesłać już dalej.

### Tracert
Polecenie służy po to jeśli chcemy się dowiedzieć przez jaką transmisje przechodzi między naszym komputerem a serwerem googla.
Pokazuje ile routerów jest po drodze.

![Alt text](https://i.ibb.co/qBQN3bZ/tracert.png "ICMP")

Rozwiązuje problemy?
- nie ma Internetu więc sprawdzam dlaczego, może kabel wyciągnięty z gniazdka
- 1, 2,3 się odzywa a potem `*`,  to gwaizdka pokazuje, że po tym ruterze 3 jest awaria...

