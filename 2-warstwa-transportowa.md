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
Oto, funkcje trójetapowego uzgadniania:
* ustala czy urządzenie jest docelowe w sieci, aktywne.
* sprawdza czy urządzenie docelowe (serwer) ma katywną usugę i akceptuje połączenie na porcie, które klient inicjuje
* informuje urządzenie docelowe żeurządzenie inicjujące zamierza ustanowić połączeniena porcie o tym numerze.

## Flagi kontrolne

**Sześć flag bitów kontrolnych to:**
* URG - flaga, która wskazuje na ważność pola pilny w nagłówku TCP;
* ACK - flaga potwierdzenia używana w ustanawianiu połączenia i zakończeniu sesji
* PSH - flaga, która oznacza wykorzystanie funkcji PUSH;
* RST - Resetuj połączenie, gdy wystąpi błąd lub limit czasu
* SYN - Synchronizuj numery sekwencji używane w ustanawianiu połączeń
* FIN - Brak więcej danych od nadawcy i używane w zakończaniu sesji

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


# Czego się nauczyłem??

## **__Transport danych__**
Warstwa transportowa służy jako łącznik pomiędzy warstwą aplikacji a warstwą leżącą poniżej, odpowiedzialną za transmisję w sieci. Warstwa transportowa jest odpowiedzialna za logiczną komunikację między aplikacjami działającymi na różnych hostach. Obejmuje TCP i UDP. Protokoły warstwy transportowej określają sposób przesyłania wiadomości między hostami i jest odpowiedzialny za zarządzanie wymaganiami niezawodności rozmowy. Warstwa transportowa jest odpowiedzialna za śledzenie konwersacji (sesji), segmentowanie danych i ponowne składanie segmentów, dodawanie informacji nagłówka, identyfikację aplikacji i multipleksowanie konwersacji. TCP jest stanowy, niezawodny, potwierdza dane, ponownie przesyła utracone dane i dostarcza dane w kolejności sekwencyjnej. Użyj protokołu TCP dla wiadomości e-mail i sieci Web. UDP jest bezstanowy, szybki, ma niski narzut, nie wymaga potwierdzenia, nie przesyła ponownie utraconych danych i dostarcza dane w kolejności, w jakiej przybywają. Użyj UDP dla VoIP i DNS.

## **__Wprowadzenie do TCP__**
TCP ustanawia sesje, zapewnia niezawodność, zapewnia dostarczanie w kolejności wysłania i obsługuje kontrolę przepływu. Segment TCP dodaje 20 bajtów narzutu jako informacje nagłówka podczas enkapsulacji danych warstwy aplikacji. Pola nagłówka TCP to porty źródłowy i docelowy, numer sekwencji, numer potwierdzenia, długość nagłówka, zarezerwowane, bity kontrolne, rozmiar okna, suma kontrolna i pilne. Aplikacje używające protokołu TCP to HTTP, FTP, SMTP i Telnet.

## **__Wprowadzenie do UDP__**
UDP rekonstruuje dane w kolejności, w jakiej są odbierane, utracone segmenty nie są wysyłane ponownie, nie ma ustanowienia sesji, a UPD nie informuje nadawcę o dostępności zasobów. Nagłówek UDP składa się tylko z portu źródłowego, portu docelowego, długości oraz pola sumy kontrolnej. Aplikacje korzystające z UDP to DHCP, DNS, SNMP, TFTP, VoIP i wideokonferencje.

## **__Numery portów__**
Protokoły warstwy transportowej TCP i UDP używają numerów portów do zarządzania wieloma równoczesnymi konwersacjami. Dlatego pola nagłówka TCP i UDP identyfikują numer portu aplikacji źródłowej i docelowej. Porty źródłowe i docelowe są umieszczane wewnątrz segmentu. Segment jest następnie enkaspulowany do pakietu IP. Pakiet IP zawiera adres IP źródła oraz adres IP miejsca docelowego. Kombinacja źródłowego adresu IP i numeru portu źródłowego lub docelowego adresu IP i numeru portu docelowego jest znana jako gniazdem (socket). Gniazdo używane jest do identyfikacji serwera i usług żądanych przez klienta. Zakres numerów portów mieści się od 0 do 65535. Zakres ten jest podzielony na grupy: dobrze znane porty, porty zarejestrowane, porty prywatne i/lub dynamiczne. Istnieje kilka znanych numerów portów, które są zarezerwowane dla typowych aplikacji, takich jak FTP, SSH, DNS, HTTP i innych. Czasem potrzebna jest informacja na temat aktywnych połączeń TCP. Netstat to ważne narzędzie sieciowe, umożliwiające ich zweryfikowanie.

## **__Proces komunikacji TCP__**
Każdy proces aplikacji działający na serwerze jest skonfigurowany do używania numeru portu. Numer portu jest automatycznie przypisywany lub skonfigurowany ręcznie przez administratora systemu. Procesy serwera TCP są następujące: klienci wysyłają żądania TCP, żądają portów docelowych, żądają portów źródłowych, odpowiadają na żądania portów docelowych i portów źródłowych. Aby zakończyć pojedynczą konwersację obsługiwaną przez TCP, potrzebne są cztery wymiany, aby zakończyć obie sesje. Klient lub serwer może zainicjować zakończenie. Trójetapowe uzgodnienie sprawdza, czy urządzenie docelowe jest obecne w sieci, czy urządzenie docelowe ma aktywną usługę i akceptuje żądania na docelowym numerze portu, z którego klient inicjujący zamierza korzystać, i informuje urządzenie docelowe, że źródło (klient) zamierza ustanowić sesję komunikacyjną na tym numerze portu. Sześć bitów kontrolnych flagi to: URG, ACK, PSH, RST, SYN i FIN.

## **__Niezawodność i kontrola przepływu__**
Aby odbiorca mógł zrozumieć oryginalną wiadomość, wszystkie dane muszą zostać odebrane, a dane w tych segmentach muszą zostać ponownie złożone w oryginalnej kolejności. Do tego celu używane są numery sekwencyjne, znajdujące się w nagłówku każdego segmentu. Bez względu na to jak dobrze została zaprojektowana sieć, zawsze pojawi się sporadyczna utrata przesyłanych danych. TCP zapewnia sposoby zarządzania utraconymi segmentami. Jednym z nich jest mechanizm retransmisji segmentów niepotwierdzonych danych. Systemy operacyjne hosta dziś zazwyczaj wykorzystują opcjonalną funkcję TCP o nazwie selektywne potwierdzenie (SACK), negocjowane podczas trójetapowego uzgadniania. Jeśli oba hosty obsługują SACK, odbiorca może jawnie potwierdzić, które segmenty (bajty) zostały odebrane w tym wszelkie segmenty nieciągłe. W związku z tym host wysyłający będzie musiał tylko ponownie przesłać brakujące dane. Kontrola przepływu wspiera mechanizm zapewnienia niezawodności transmisji TCP, przez dostosowanie tempa przepływu danych między nadawcą a odbiorcą. Aby to osiągnąć, nagłówek TCP zawiera 16-bitowe pole zwane rozmiarem okna. Proces wysyłania potwierdzeń przez odbiorcę podczas przetwarzania odebranych bajtów i ciągłe dostosowywanie okna wysyłania źródła jest znane jako okna przesuwne. Źródło może przesyłać 1460 bajtów danych w każdym segmencie TCP. Jest to typowy MSS, który może otrzymać urządzenie docelowe. Aby uniknąć i kontrolować zatory, TCP wykorzystuje kilka mechanizmów obsługi zatorów. Źródło zmniejsza liczbę niepotwierdzonych bajtów, które wysyła, a nie rozmiar okna określony przez miejsce docelowe.

## **__Komunikacja z użyciem UDP__**
UDP jest prostym protokołem, który zapewnia podstawowe funkcje warstwy transportowej. Gdy datagramy UDP są wysyłane do miejsca docelowego, często podążają różnymi ścieżkami i docierają w niewłaściwej kolejności. Protokół UDP nie znakuje segmentów przy użyciu numerów sekwencyjnych, tak jak robi to TCP. Stąd protokół UDP nie ma możliwości uporządkowania odebranych datagramów według kolejności ich nadawania. Protokół UDP po prostu scala dane w kolejności ich otrzymania i przekazuje do aplikacji. Jeśli kolejność danych jest ważna dla aplikacji, musi ona sama zidentyfikować (lub zinterpretować) właściwą ich kolejność i sposób przetwarzania. Aplikacje Serwerowe oparte na UDP mają przypisane dobrze znane lub zarejestrowane numery portów. Kiedy protokół UDP otrzymuje datagram adresowany do jednego z tych portów, na jego podstawie, przekazuje odebrane dane do odpowiedniej aplikacji. Aplikacja klienta, wykorzystującego protokół UDP, losowo wybiera numer portu z zakresu portów dynamicznych i używa tego numeru jako portu źródłowego dla tej komunikacji. Port docelowy będzie zwykle z grupy dobrze znanych lub zarejestrowanych portów, który z kolei przyporządkowany jest usłudze na serwerze. Kiedy klient ustali numery portów źródłowego i docelowego, te same numery portów użyte zostaną w odpowiedzi serwera. Oczywiście numery tych portów w nagłówku datagramu, stanowiącego odpowiedź serwera do klienta, będą zamienione miejscami.
