# Warstwa transportowa

## __Zadania warstwy transportowej:__
* **śledzenie indywidualnych konwersacji** - w tej warstwie każdy zestaw danych przepływający między aplkacją źródłową a docelową nazywany jest konwersacja i jest śledzony osobno. Funkcją w.transportowej jest utrzymanie i śledzenie konwersacji. Host (komputer PC) możze mieć wiele aplikacji komunikujących się w sieci jednocześnie (email, whatsapp, www, widoe czat, youtube)
* **segmentacja i powtórne składanie pakietów dnych** - dane aplikacji dzielone są na bloki o odpowiedniej wielkości, co jest obowiązkiem warstwy transportowej. Bloki te nazywane są _segmentami_ lub _datagrami_, w zależności o użytego protokołu. Wówczas bloki te, są łatwiejsze do zarządzania i transportu.
* **dodawanie informacji nagłówka** - protokły warstwy transportu dodają informację nagłówka, które zawierają dane binarne zorganizoane w kilka pól. Nagłowek wykorzystywany jest przez host odbierający do ponownego złożenia bloków danych w kompletny strumieńdanych dla warstwy aplikacji.
  Przy wielu aplikacjach uruchomionych jednocześnie, dane docierają poprawnie do każej z aplikacji.
* **identyfikacja apikacji** -  warstwa transportu musi w jednym czasie zarządzać wieloma połączeniami jednocześńnie i dzielić dane, które należa do różnych aplikacji. Warstwa transportu  identyfikuję aplikację docelową za pomocą  id zwanego numerem portu.
* **multipleksowanie konwersacji** - umożlwia przeplatanie wysyłanych danych, wideo, www, voip

## __Protokół TCP__
TCP uważany jest za "wiarygodny", który gwarantuje dostarczenie wiadomości
* **Protokół TCP dzieli dane na segmenty**
* transport z użyciem TCP można porównać jako transport, gdzie pakiety są śledzone od źródła do celu
* jest wolniejszy od UDP, bo są potwierdzenia itp...

  TCP zapewnia niezawodność i kontrolę przepłwu za pomocą:
  * numerowania i śledzenie segmentów
  * potwierdzanie odbioru danych
  * ponowne przesyłanie niepotwierdzonych danych po upływie okreslonego czasu
  * sekwencjonowanie danych, jeśli pojawią się w złej kolejności
  * wysyłanie danych w odpowiednim tempie, który jest akceptowalny przez odbiorcę

W celu utrzymania stanu konwersacji i śledzenia informacji, TCP musi najpierw ustanowić połączenie między nadawcą a odbiorcą - dlateog uwżany jest jako protokół połączeniowy.

## __Protokół UDP__
* nie zapewnia niezawodności i kontroli przepływu, wiec wymaga mniejszej liczby pól nagłowka
* datagramy UDP mogą byc przetwarzanie szybciej niż segmenty TCP
* jest protokołem bezpołączeniowym
* nie zapewnia niezawodności i kontroli przepływu więc nie wymaga zestawienia połączenia  jak TCP
* nie ślezdi informacji wysyłanych i odbieranych między klientem a serwerem
* znany również jako _protokół działający na zasadzie najlepszych środków (best-effort)_ , czyli nie ma potwierdzeń żę dane są odbierane w miescu docelowym
* brak potwierdzeń

Można porównać działanie UDP do zwyklego listu - czyli nadawca nie jest świadomy czy czy lsit dotrze do odboircy

## Problemy warstwy transportowej:
* film, który zajmuje 60GB 4K, MKV pojawiają sie problemy i jak to rozwiązać

* jeśli film byłby wysłany w całości przez interfejs sieciowy, to niebylibyśmy w stanie zrobić nic innego np. sprawdizć poczty, fb, strony informacyjnych... a tutaj jeszcze 1,5h wysyłania. Cała sieć domowa LAN przestaje działać.
Np. idziemy na pocztę z wielkim obrazem ale nie da się go wysłać bo jest za duży, trzeba go podzielić na mniejsze części.

Załóżeniem w.transportowej jest to, że jeśli mamy wiadomość, to mamy mechanizm segmentacji, czyli podzielenie danych na mniejsze cześci.
Te kawałki są tak małe, że mamy złudzenie optyczne, że w danym momencie jest wysyłany tylko ten film, yt, messenger, mail, a tak na prawdę w tanej jednostce czasu jest wysyłany tylko jeden segment, ale są przeplatane trochę tego, tamtego  i w rezultacie widzimy jakby to wszystko od razu było uploadowane.

* czy plik doszedł czy nie doszedł, albo doszło tylko 80% ze 100%. Rozwiązaniem sprawdzenia czy coś doszło w TCP jest taki mechanizm **potwierdzeń i retransmisji** w UDP nie ma.
mechanizm **potwierdzeń i retransmisji** to: że jeśli ja wyślę jakiś kawałek wiadomości (segment) jako nadwaca to oczekuje, że dostanę potwierdzenie od odbiorcy, że otrzymał odbiuorca i czekam na to potwierdzenie przez określony czas. Jak nie doszło, to robię retransmije i wysyłam jeszcze raz, ale one są złe i dobre...
Potwierdzenie w TCP to ACK (Acknowledge)

*kolejny problem to  wysyłam pakiety 1,2,3,4,5,6 ale do odbiorcy dojdzie w innej kolejności np 1,2,6,5,4,3 i teraz to trzeba poukładać. Skąd mamy wiedzieć, że zostanie to poprawnie poskładane w jedną całośc? Otóż, każda cześć pliku czyli segment dostaje unikalny **numer sekwencyjny**
![Alt text](https://i.ibb.co/kX4G1XG/sekwencyjne.png "a title")
## Jakie są protokoły?
*W obu protokołach dane są dzielone na kawałki w taki sam sposób, z małymi drobnymi niuansami...
* TCP
* UDP

## **TCP**
### nawiązanie połączenie TCP

* 1. Klient wysyła żadanie zainicjowania sesji klient-serwer z serwerem (chce korzystać z Twoich uslug, czy mogę? )
* 2. Serwer przyjmuje sesję komunikacyjną klient serwer i wysyła żadanie zainicjowania sesji komunikacyjnej serwer-klient (serwer mówi, tak, niech będzie, zgadzam się, działamy?)
* 3. Klient inicjujący potwierdza sesję komunikacyjną z serwera ( no to działamy)
![Alt text](https://i.ibb.co/b3f3WQc/connecttcp.png "a title")

Klient wysyła segment z pustą kopertą z 1 w polu SYN, apikacja serwerowa jak się zgodzi to odsyła pustą kopiertę, gdzie są dwie flagi SYN i ACK

### Zakończenie sesji TCP

* 1. Kiedy klient nie ma więcej danych do przesłąnia wysyła segment z ustawioną flagą FIN.
* 2. Aby potwierdzić otrzymanie segmentu z ustawioną flagą FIN, serwer wysyła segment z ustawioną flagą ACK, co końćzy połączenie od klienta do serwera.
* 3. W celu zakońćzenia sesji od serwera do klienta serwer wysyła segment z ustawioną flagą FIN do klienta.
* 4. Aby potwierdzić otrzymanie segmentu z ustawioną flagą FIN od serwera, klient odpowiada segmentem z ustawioną flagą ACK.

![Alt text](https://i.ibb.co/TBbBHXf/finishtcp.png "a title")

**UDP**
W UDP nie ma nawiązania i zakońćzenia sesji, to kawał chama.

### Porównianie z życia TCP i UDP
Wygląda to tak:

#### TCP
Cześć, brat, jestes w domu, 
Jestem
CHciałbym wpasć do Ciebie, mogę?
Możesz
Ok, to będę
Ok

#### UDP
To cham, nie pyta się przyjeżdza do brata, pomimo, że nie może to tak to wygląda

# Three way handshake

# Flagi kontrolne

# Mechanizm portów
Skąd warstwa transportowa ma wiedzieć, do któej aplikacji w ramach w.aplikacji ma przekazać.
Rozwiązanie tego problemu jest takie samo w TCP i UDP  - to PORTY są to numery 80, 2055

Dzięki portom możemy zarządzać wieloma, jednoczesnymi konwersacjami.

Pola nagłówka TCP i UDP identyfikują numery portów aplikacji źródłowej i docelowej. Mamy więc:
* port źrodłowy (16)
* port docelowy (16)

Port źródłowy powiązany jest z aplikacją źródłową na hoście loklanymm a numer portu docelowego jest z aplikacją docelową (serwer www, ftp...)

**Pary gniazd (socket)** jest to kombinacja adresu IP i numeru portu (źrodłowy i docelowy)

Gniazdo używane jest do identyfikacji serwera i usług żądanych przez klienta. Przykładowe gniazdo u klienta, reprezentujące port 1099 może mieć postać: 192.168.1.5:1099
Natomiast gniazdo docelowo na serwerze może wyglądać tak: 192.168.1.7:80
Razem, obydwa tworzą parę gniazd: 192.168.1.5:1099, 192.168.1.7:80
Gniazda umożliwiają rozróżnianie wielu procesów działających u klienta oraz rozróżnianie wielu połączeń z procesami serwera.

Porty jest podobieństwem do mieszkania.
Adresy IP są blokiem mieszkalnym

Zawsze klient łaczy sie z aplikacją serwera a nie na odwrót.
Aplikacja kliencja zarezerwuje sobie dowolny nie zarezerwowany port

![Alt text](https://i.ibb.co/7ry9spm/porty.png "a title")

Dobrze znane porty i porty zarejestrowane są przeznaczone dla aplikacji serwerowych.
Skąd wiadomo na jakim porcie ma pracować aplikacja serwerowa?
Bo porty nie są przydizelanie dla semej aplikacji jako tako, porty sa przydzielane protokołowi w.aplikacji.
IANA dla protokołu HTTP przydzieliła port 80, dla HTTPS port 443.

Dlaczego 80? A dlaczego masz na imię Maciej? Bo rodzice tak chcieli - IANA robiłą to w ten sam sposób.

# Polecenie netstat
Nieznane połączenie TCP mogą być naruszeniem bezpieczeńśtwa, mogą wskazywać, że ktoś nasłuchuje a nie powinien.

`netstat - nab` polecenie  pokazuje wszystie połączenia stan LISTENING czyli coś nasłuchuje, aplikacja serwerowa??
ESTABLISHED to znaczy że połączenie nawiąane przez nas, my połączyliśmy sie z kimś

```
C:\> netstat
Active Connections
  Proto  Local Address          Foreign Address            State
  TCP    192.168.1.124:3126     192.168.0.2:netbios-ssn    ESTABLISHED
  TCP    192.168.1.124:3158     207.138.126.152:http       ESTABLISHED
  TCP    192.168.1.124:3159     207.138.126.169:http       ESTABLISHED
  TCP    192.168.1.124:3160     207.138.126.169:http       ESTABLISHED
  TCP    192.168.1.124:3161     sc.msn.com:http            ESTABLISHED
  TCP    192.168.1.124:3166     www.cisco.com:http         ESTABLISHED
(output omitted)
C:\>
```


Każda osobna karta w Chromie to  inny port

Nagłówki to to co wypisujemy na kopercie.
Numer portu źródłowego i numer portu docelowego
Numer sekwencyjny
NUmer potwierdzenia
Flagi kontrolne (FIN, ACK, RST....)

# Mechanizmy kształotowania ruchu
Jest w  TCP a nie ma w UDP

![Alt text](https://i.ibb.co/zbBmQkd/oknoprzesuwne.png "a title")
