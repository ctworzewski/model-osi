# Warstwa transportowa

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


Porty jest podobieństwem do mieszkania.
Adresy IP są blokiem mieszkalnym

Zawsze klient łaczy sie z aplikacją serwera a nie na odwrót.
Aplikacja kliencja zarezerwuje sobie dowolny nie zarezerwowany port

![Alt text](https://i.ibb.co/7ry9spm/porty.png "a title")
