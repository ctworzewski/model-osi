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
  
W IPv6 nazywa się to inaczej, ale idea jest taka sama- mówimy o tym samym.
