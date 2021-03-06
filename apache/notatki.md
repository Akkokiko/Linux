# Teoria

***Apache***
to serwer sieciowy zapewniający nam znaczną większość funkcjonalności, które wykorzystujemy używając Internetu. Może zostać użyty do przesłania dowolnego typu plików.

***Protokół HTTP***  
Zasady wymiany informacji i współpracy programów: klienta i serwera. Klient wysyła żądania. HTTP jest bezstanowy (zapytania mogą być zrozumiane w oderwaniu od pozostałych). Każde żądanie powiązane jest z zasobem. Zasobem może być obrazek, strona HTML czy plik z kodem JavaScript (protokół HTTP nie określa czym dokładnie jest 
zasób, ale sposób w jaki można dostać się do zasobu).

Każdy zasób ma swój unikalny identyfikator (URI).  

***Komunikacja HTTP***  
Komunikacja HTTP oparta jest na żądaniach i odpowiedziach.   


***Metody komunikacji***
```
GET
pobieranie zasobu wskazanego przez URL
HEAD
pobiera informacje o zasobie (czy zasób jest dostępny)
PUT
przyjęcie danych od klienta przez serwer kiedy znasz adres URL
POST
przyjęcie danych od klienta przez serwer kiedy nie znasz adresu URL
DELETE
usunięcie zasobu
OPTIONS
informacje o opcjach i wymaganiach
TRACE
diagnostyka, analiza kanału komunikacyjnego
CONNECT
przeznaczone  dla serwerów pełniących funkcje tunelowania
PATCH
aktualizuj dane
```



# Praktyka
***Przed instalacją***  
Poprawnie skonfigurowana sieć.
Dokładny czas systemowy maszyny jest ustawiony na synchronizację z serwerem czasu.
Zainstalowane są najnowsze aktualizacje zabezpieczeń.
Domyślny port serwera WWW (80) jest otwarty w zaporze.

***Instalacja***  
Instalacja oprogramowania lamp server (w yast ->  oprogramowania-> wyszukaj “Web and LAMP Server”)
Uruchom apache2 (cmd: sudo systemctl start apache2 )

***Konfiguracja***  
	Pliki konfiguracyjne:
		/etc/sysconfig/apache2 - plik przechowujący globalne ustawienia
		/etc/apache2/

***Konfiguracja virtual hosta***  
	cmd: apache2ctl -S - wyświetlanie informacji o virtual host
	Folder /etc/apache2/vhosts.d/ - zawiera szablony plików konfiguracyjnych.
	Pojęcia:  
- ServerName - nazwa domeny
- DocumentRoot - ścieżka do katalogu, z którego Apache powinien udostępnić pliki tego hosta
- ServerAdmin - adres email administratora
- ErrorLog - plik dziennika dla błędów
- Custom Log - ogólny plik dziennika
- <Directory “document root”> - konfiguracja katalogu z plikami

***Tworzenie  virtual host***
1. w pliku  /etc/hosts -  w linijce zaczynającą się 127.0.0.1 dodajemy nazwe nowego hosta (np. www.example.com)
2. tworzymy katalog hosta wirtualnego (/srv/www/vhosts/nazwa_hosta)
3. w tym katalogu tworzymy plik index.html i wypełniamy go typowo na html
4. w folderze vhosts.d kopiujemy plik vhost.template i nadajemy mu nazwę nazwa_hosta.conf
5. W skopiowanym pliku wprowadzamy zmiany:
  - ServerAdmin = webmaster@.nazwa_hosta.com
  - ServerName = www.nazwa_hosta.com
  - W ostatniej!!!!!!!! sekcji Directory = ścieżka do katalogu hosta
  - DocumentRoot = /srv/www/vhosts/nazwa_hosta
6. Resetujemy apache2 systemctl restart apache2
