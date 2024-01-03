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

**TCP**
**UDP**

