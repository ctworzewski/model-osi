# warstwa aplikacji w TCP/IP

Będę opisywał czym jest, jak działa, przykłady użycia. Jest to tylko gromadzenie mojej wiedzy z notatkami. Więc błędy mogą się zdarzyć.

**Warstwa aplikacji w modelu TCP/IP składa się z:**

* warstwy aplikacji
* warstwy prezentacji
* warstwy sesji

Co sie w nich dzieje opowiem za chwilę w kilku słowach...

## Warstwa aplikacji
Warstwa ta jest najbliższa człowiekowi, jest to po prostu działanie aplikacji typu Thunderbird, Outlook, Messanger, Chrome
najczesciej *warstwa aplikacji* jest aktywowania w momencie wciśnięcia przycisku **Enter**.

Działają w niej **protokoły** np: DNS, SMTP, POP, IMAP, RDP, FTP...

### Jaki jest problem warstwy aplikacji?
Taki, iż kiedyś człowiek się zastanasiał jak stworzyć coś, żeby załadować muzykę, film, wysłać zdjęcia, przerzucić nas na inną stronę www, wysłać wiadomość - kiedyś tego nie wiedziano, teraz jest to oczywiste.
Aplikacje działają w różnych architekturach: P2P oraz klient-serwer. 

To programista musi odpowiednio zaprogramować aplikacje z wykorzystaniem tych architektur. 
Obrazowo Chrome jest stworzony w aplikacji klient-serwer, wysyła dane do serwera storn www, który jest oddalony o setki kilometrów od nas. Podobnie jest z Outlookiem.

Można to porównać z tradycyjną Pocztą Polską -> chcemy wysłać li do cioci z Ameryki (piszemy go) w w.aplikacji tez tworzymy wiadomość, którą kierujemy np. do serwera www, że chcemy taką a nie inną stronę.

## Warstwa prezentacji
Odpowiada za prezentowanie danych na odpowiedni format danych tj. MOV, PNG, MKV,MP4, JPG. Odpowiada również za kompresje danych, tak, aby przesłąć mniejszy plik niż on faktycznie zajmuje.
Np. jeśli próbujesz otworzyc plik o nazwie **cezary.pdf** możesz go otwrzyć, ponieważ zapewne posiadasz odowiednie aplikacje do tego, który jest typ pliku PDF obsługują.
Odpowiedzialna jest również za szyforwanie danych, tak, aby wysyłane i odbierane dane były bezpieczne i niewidoczne dla **black hat**.

## Warstwa sesji
Odpowiedzialna jest za rozpoczęcie rozmowy np: klienta www z serwerem stron. Weryfikuje, uwierzytelnia klienta, czy może się połączyć.
Warstwa sesji, jak sugeruje jej nazwa, jest odpowiedzialna za tworzenie i utrzymywanie sesji komunikacyjnych pomiędzy aplikacjami: źródłową i docelową. 
Warstwa sesji prowadzi wymianę informacji: rozpoczyna konwersacje, utrzymuje ich aktywność i wznawia je, jeśli zostały utracone lub są od dłuższego czasu bezczynne.
