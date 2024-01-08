# warstwa łącza danych

## Topologia fizyczna i logiczna
Topologia sieci to schemat zawierający wzajemne relacje urządzeń sieciowych oraz połączenia między nimi.

Istnieją dwa rodzaje topologii używane podczas opisywanych sieci:
* **topologia fizyczna** - pokazuje połączenia fizyczne i sosób, w jaki urządzenia są ze sobą połączone
  * topologia LAN
    * miagistrala - karta sieciowa bnc, używanie terminatrów i złączek typu T; kabel idzie od PC do PC; medium transmisyjne współdzielone, problem z przepustowością; tutaj dochodzi do kolizji
    * pierścienia - to taka magistrala,bo idzie jeszze kabel od osatniego do pierwszego.
    * gwiazdy - gwiazda to połączenie za pomocą switcha
      
* **topologia logiczna** - identyfikuje wirtualne połączenia między urządzeniami za pomocą interfejsów urządzeń i schematów adresowania IP.
Można powiedzieć, że topologie logiczne rozwiązuje problem rywalizacji i nie dochodzi do kolizji


## Jakie jest przeznaczenie warstwy łącza danych?
* warstwa łącza danych jest odpowiedzialna za komunikację między kartami interfejsu sieciowego urządzęń końcowych
* umozliwia protokołom wyższej warstwy  dostęp do nosnika warstwy fizycznej i enkapsuluje pakiety warstwy 3 (iPv4 i IPv6) w ramkach warstwy 2
* realziuje również wykrywanie błędów o odrzuca wszelkie uszkodzone ramki.

## Adresy MAC
* Adres MAC składa sie z 48-bitów, wyrażoną za pomocą 12 wartości szesnastkowych
* pierwsza cześć MAC to adres OUI (czyli producenta) a druga część to unikatowy numer karty sieciowej

## Nagłówki Ethernet

![Alt text](https://www.minitool.com/images/uploads/2020/04/ethernet-frame-1.jpg "a title")

* Preambuła.. co to? Po co?
  To 8 bajtów, gdzie mamy 010101**11**, po co to jest? Po to aby można było sie dowiedzieć gdzie się kończy jedna ramka, a gdzie zaczyna druga ramka Ethernet oraz żeby można było na bazie preambuły dostosoweać do prędkości transmisji z jaką jest to do nas wysyłane
* mamy adres docelowy MAC adres i dopiero źrodłowy. W warstwie sieci, najpierw był źrodłowy, a potem docelowy
* Type - tutaj wpisujemy np, że to taki protokół IPv4, albo ARP. Jaki protokół warstwy wyższej jest umieszony w polu Dane (Data). Tam już mamy pakiet IPv4, v6, do którego protokołu w.wyższej należy przekazać to co mamy w polu Data.
* CRC - suma kontrolna, która pozwala nam wykryć czy ta ramka, która do nas przyszła nie uległa uszkodzeniu po drodze.

  Najważniejsze to: **docelowy adres MAC** a potem **źrodłowy adres MAC**

  Źrodłowy to wiadomo bo to mój komputera, a docelowy to jaki to nie wiem :)
  Musze się dowiedzić jaki jest docelowy, ale jak?

  W kontekście protokołu IPv4, mamy do tego taki protokół któy nazywa się **protokołem ARP**

  ## Protokół ARP
  Działa bardoz prosto:
  wysyłamy zapytanie w sieć, czy jesteś komputerze co masz taki adres IP, jak jesteś to przyślij mi swoj adres MAC.
  To wszystko jest wysyłane rozgloszeniowo - do wszystkich!
  Jeśli jest wysyłane do wszystkich... a przecież teraz to zapytanie ARP umieszczane jest w ramce Ethernet, to skąd wiaodmo jaki adres docelowy MAC jest używany. Używa się adresu MAC rozgłoszeniowego, który wygląda tak: **ff:ff:ff:ff:ff:ff** same jedynki.

  Żeby oszacować, czy PC jest w sieci lokalnej, jeśli poza to w ramach protkołu ARP zrealizuje się to zapytanie, ale o adres bramy domyślnej. 


## Przełączanie w sieciach Ethernet

Siłą nowego Ethernetu są urządzenia zwane SWITCHAMI
Rolą koncetratora jest taka sama jak switcha. Miał podobną logikę, dzielił sieć na różne segmenty.

Dzięki PRZEŁĄCZNIKOWI transmisja jest full-duplex - TX i RX jest taka sama.

### Przełącznik posiada tablice adresów MAC
  
  
  

