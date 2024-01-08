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

