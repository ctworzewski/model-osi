# warstwa sieci

Warstwa aplikacji stworzyła wiadomość, potem przesłało to do warstwy transportowej - z kolei warstwa transportowa podzieliła wiadomość na segmenty lub datagramy, nadała port źrodłowy i docelowy, numery sekwencyjne...
Wszystko pięknie, bo teraz wiadomo do jakiej aplikacji ma to zostać przesłane, **ale nie wiadomo do jakiego urządzenia**. 
Obecnie jest tylko jedna kopera z portem src i dst.

Warstwa sieci pojawia się protokół IPv4 i IP-v6.

Głownym problem warstwty sieci, jes to, że musi ona ogarnąć jak ma wyglądać komunikacja pomiędzy sieciami lokalnymi. Musimy powiedzieć do którego urządzenia wysłać.

Więc jeśli problemem jest to w jaki sposób wysałać to do punktu B, kóry znajduje się na drugim końcu świata - jak to połączyć??
Trzeba było wymyślić jakiś adres nakladkowy i tym adresem nakładkowym jest adres IP.

## Budowa IP 

Każdy adres IP skłąda sie z dwóch cześci: 
* **cześci sieci**,
* **części hosta**.

* część sieci - tocoś takiego co jest wspólne dla wszystkich komputerów, które są w danej sieci lokalnej.
  Wszystkie komputery w sieci lokalnej mają ten sam początek adresu IP

Komputer nie widzi 192.168.2.1.
Komputer **widzi** adres 32-bitwy - komputer widzi 0 i 1.

Nie chcielbiysmy wpisyuwać adresu 1110000.100001.00000010.00001010

Ilośc adresów IP?  = 2^32 około 4 miliardów, tyle adresów na potrzeby całego świata.

Jeśli czesć sieci będzie 16bitowa, to 16 bitów będzie na adresacje hostów.

Skąd wiadomo, jesli liczba ma 32bity to gdzie sie kończy czesć sieci, a gdzie zaczyna się częsci hosta - to właśnie wyznacze jest przez **maskę podsieci**.
Tam gdzie są same 1 to to będzie część sieci
Zawsze najpierw są 1 a potem 0-ra.

# Formaty zapisu maski podsieci
* format krótki - /9  zliczamy 1 binarne
* format długi - 255.128.0.0

Im maska krótka /9 mniejsza tym więcej hostów można zaadresować, jeśli większa np. /24 to mniej hostów.

### Jak zrealizować komunikację pomiędzy sieciami lokalnymi?
Komputer jeżeli wie , że ten drugi nie jest w  jego sieci lokalnej, to wie, że sam sobie nie poradzi to musi to wysłać to bramy domyślnej routera.
Skąd PC wie, że ten drugi nie jest w jego lokalnej?

Co robi ruter, że wie co ma zrobić dalej?
Rutery stanowią na swój sposób logikę skrzyżowań. Tymi skrzyżowaniami są rutery,  kable idą od rutera do rutera.
Jeśli dojdzie to do rutera to teraz on musi wiedzieć co z tym zrobić dalej.

Planujemy jechać z Kielc do Torunia... ale jak
Wsiadamy do auta jedziemy do pierwszego skrzyżowania, i co teraz prosto w lewo czy prawo?
Na skrzyżowaniu są DROGOWSKAZY one mówią gdzie jechać
Jesli pakiet wpływa do rutera to teraz gdzie go przesłać, mam kilka kabli, gdzie go przesłać co teraz?
Drogowskazami w ruterach jest tablica routingu.

**Routing** to jest **proces podejmowania decyzji odnośnie tego, któym interfjesem należy ten pakiet wypuścić** aby dojechał do wlasciwej sieci lokalnej i urządzenia końcowego

![Alt text](https://i.ibb.co/DgzJRZt/arp.png "a title")

Na rysunku - słuchaj stary jeżeli będziesz miał teraz pakiet zmierzający do takiej podsieci `192.168.10.0 255.255.255.0` to wyppuść go tym interfejsem `192.168.10.10`, zawsze jest podawany adres sieci z maską sieci

W IPv6 nazywa się to inaczej, ale idea jest taka sama- mówimy o tym samym.


## Wprowadzenie do routingu

### Routing statyczny
 ### **Charakterystyka trasy statycznej:**
 * musi być skonfigurowany ręcznie
 * musi być ręcznie dostosowana przez admina jeśli nastapi zmiana topologii sieci
 * dobra dla małych sieci bez nadmiarowości
 * * jesli będzie awaria, autoamtycznie znajdzie alternatywną trasę

### Routing dynamiczny
### Dynamiczne routing automatycznie:
* odkryje zdalne sieci
* zaktualizuje informacje o trasach
* wybierze najlepszą ścieżkę do miesjca docelowego
* znajdzie nowe najlepsze ścieżki, gdy nastapi zmiana topologii
* jesli będzie awaria, autoamtycznie znajdzie alternatywną najlepszą trasę.

Trzeba powiedzieć tak: słuchaj stary, chciałbym abyś do tablicy routingu  dodał nową trasę do tablicy routing, i ta trasa będzie mówić, że jeśli dostaniesz pakiet, który należy do takiej a nie innej podsieci czyli `10.1.1.0 255.255.255.0` to wyślij go tym interfejsem, albo adresem następnego przeskoku `209.165.200.226`

![Alt text](https://i.ibb.co/0Q6n2MZ/nexthop.png "a title")

Co to jest next hop?
To jest następny przeskok, przeskokiem jest skakanie od routera do rutera.

Dla małych sieci jest ok, ale dla 15-20 routerów kiepsko.
Mamy też alternatywne trasy do punktu, i trzeba ręcznie dodać alternatywy, bo jeśli na danej trasie będzie  awaria to trzeba mieć alternatywne połączenie.
 Skąd się biorą wpisy w tablicy routingu?



 Są 3 spospoby na to skąd się biorą wpisy w tablicy:
 * wpisałem z palca ten wpis, to sie nazywa **routing statyczny**
 * routing dynamiczny


### Istnieją trzy rodzaje tras w tablicy routingu routera:
* **bezpośrednio przyłączone** - trasy te są automatycznie dodawane przez router, pod warunkiem, że interfejs jest aktywny i ma adresowanie
* **zdalne**
  * **dynamicznie** - za pomocą protokołu routingu
  * **ręcznie** - przy pomocy trasy statycznej
* **domyślna trasa** - przesyła cały ruch w okreslonym kierunku, gdy nie ma dopasowania w tablicy routingu

## Adresowanie IPv4

O tym gdzie kończy sie cześć sieci adresu IP mówi  maska podsieci

### Rodzaje adresów IPv4
* **publiczne**
  * 
* **prywatne**
  * adresy prywatne to bloku adresów używanych przez większość organizacji do przypisywania adresów IPv4 do hostów wewnętrznych
  * prywatne adresy IPv4 ie są unikalne i mogą być używane wewnętrznie w dowolnej sieci
  * adresy prywatne nie są globalnie rutowane
    ![Alt text](https://i.ibb.co/0K3BBS1/privateip.png "a title")

