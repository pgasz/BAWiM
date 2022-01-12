# Bezpieczeństwo aplikacji webowych i mobilnych - projekt
W tym tepozytorium znajduje się projekt na zaliczenie powyżej wymienionego przedmiotu. Zawiera ono prezentację, treści zadań oraz instrukcje instalacji niezbędnych pomponentów do ich wykonania.

### Autorzy
- [Gasz Paweł - pgasz](https://github.com/pgasz "Gasz Paweł - pgasz")
- [Duda Krzysztof - krzysztofd1235](https://github.com/krzysztofd1235 "Duda Krzysztof - krzysztofd1235")

## Testowanie podatności wybranych aplikacji webowych na ataki typu Cross-side scripting (XSS)

### Zadania do wykonania
####Zadanie 1
#####Przygotowanie do zadania 1 
- Włącz  [google gruyere](https://google-gruyere.appspot.com/start "google gruyere")
- Zapisz swoje Gruyere ID
- Wejdź do aplikacji i zarejestruj kilku użytkowników (nie używaj prawdziwych haseł ponieważ aplikacja jest bardzo dziurawa)

##### Polecenia
##### 1.1 Atak reflected XSS 

Aby wykonać to zadanie, należy znaleźć na stronie miejsce, gdzie jest możliwe wykonanie ataku reflected XSS. Należy wstrzyknąć kod JavaScript i wyświetlić ciasteczka użytkownika. W odpowiedzi należy podać użyty kod oraz screen potwierdzający autentyczność rozwiązania.

##### 1.2 Atak stored XSS

Aby wykonać to zadanie, należy znaleźć miejsce, w którym można dodać jakiś wpis widoczny dla wszystkich użytkowników. Następnie należy w nim umieścić kod wyświetlający ciasteczka danego użytkownika. Aby sprawdzić, czy kod działa poprawnie, należy zalogować się na innego użytkownika i sprawdzić, czy po wejściu na odpowiednią stronę na ekranie zostaną wyświetlone ciasteczka. W odpowiedzi należy podać użyty kod oraz screen potwierdzający autentyczność rozwiązania.

####Zadanie 2
#####Przygotowanie do zadania 2
- Do zadania drugiego będzie niezbędne konto na portswiggerze
- w zadaniu będziemy posługiwać się programem Burp. Aby zintegrować przeglądarke z Burpem można posłużyć się [instrucją z laboratorium](https://github.com/djuszka/BAWiM_lab_2021/blob/main/BAWiM_lab2.md#user-content-zadanie-2-konfiguracja-przeglądarki "instrucja z laboratorium") 

##### Polecenia
##### 2.1 Atak DOM XSS

Zadanie to polega na wykorzystaniu luki w zabezpieczeniach strony, która wykorzystuje niebezpieczną funkcję document.write do zapisywania danych na stronie. Funkcja ta wykorzystuje dane z location.search, którymi można sterować za pomocą adresu URL witryny. Co można wykorzystać w ataku.

##### 2.2 Atak reflected DOM

W tym przykładzie serwer przetwarza dane z żądania i powtarza je w odpowiedzi. Tworzy się w ten sposób niebezpieczna luka, która można wykorzystać. Aby wykonać to zadanie, należy wstrzyknąć kod, który wywoła funkcję alert().

####Zadanie 3
#####Przygotowanie do zadania 3
- Instrukcja do instalacji aplikacji DVWA znajduje się na githubie z projektem
##### Step by step installation
###### On Windows
We recommend running the app with xampp:
* download and install xampp (Apache + Mysql + PHP): https://www.apachefriends.org/index.html
* download and unzip DVWA: http://dvwa.co.uk/
* open xampp -> explorer -> htdocs and delete all files, create new folder named dvwa, then move there all downloaded DVWA files
* go to config folder (one of those, that have been moved) and change the name of the main config file `config.inc.php.dist` -> `config.inc.php`
* modify the config file with notepad or other similar tool and change the default passowrd to blank, like that: `$_DVWA['db_password']='';`
* run the Apache and Mysql servers
* run the web browser- we highly recommend __Firefox__, since some features don't work on other browsers, e.g. chrome
* try to sign in into admin account- the default credentials should be `admin:password`
* at the bottom of the page, __Setup / Reset DB__ tab on the left, try to __Create / Reset Database__
* if you didn't receive any error message, you can skip all the next steps and go to the exercises
* if so, stop Apache and Mysql servers
* go to Mysql -> config -> my.ini
* add the following line `skip-grant-tables` right under `[mysqld]`, it should look like that:
```
(...)
# The MySQL server
default-character-set=utf8mb4
[mysqld]
skip-grant-tables
port=3306
(...)
```
* run Apache and Mysql servers again and repeat previous steps, now you should be able to setup your database and start exercises.

###### On Linux
* `sudo apt-get update`
* `sudo apt-get dist-upgrade`- it will take a few minutes.
* `sudo apt install apache2` 
* `sudo apt-get install git` 
* `sudo apt install mysql-server` 
* `sudo apt install php` 
* `sudo apt install php-mysql`
* `cd /var/www/html`
* `sudo git clone https://github.com/ethicalhack3r/DVWA`
* `sudo chmod -R 777 DVWA`
* `sudo mv DVWA dvwa`
* Now you need to edit the configuration file, e.g. `sudo nano DVWA/config/config.inc.php.dist`, replace the password value with blank: `$_DVWA['db_password']='';` and username with _root_: `$_DVWA['db_user']='root';`. Save the file as __config.inc.php__
* `sudo service mysql start`
* `sudo mysql -u root -p` and leave the password field blank
* inside mysql shell `create user 'root'@'127.0.0.1' identified by '';`
* also inside mysql shell `grant all privileges on dvwa.* to 'root'@'127.0.0.1';`, then `\q` to exit
* `cd /etc/php/<version_named_directory>/apache2`
* configure `php.ini`, e.g. `sudo nano php.ini`
* search for _allow_url_ (inside nano- ctrl+w), both _allow_url_include_ and _allow_url_fopen_ values should be set to _On_
* `sudo service apache2 start`
* run the web browser- we highly recommend __Firefox__ and go to `http://127.0.0.1/dvwa/setup.php`
* at the bottom of the page, __Setup / Reset DB__ tab on the left, try to __Create / Reset Database__
* you should be redirected to `http://127.0.0.1/dvwa/login.php`. Sign in, default credentials are `admin:password`
* now you should be able to start the exercises


- Instalacja WSL na Windowsa 
Aby włączyć tą funkcje wyszukujemy w wyszukiwarce systemowej wyszukujemy "funkcje systemu windows" i wybieramy pierwszą pozycje. 
Pojawi się nowe okienko, zjeżdżamy odrobinę na dół i wybieramy "podsystem windows dla systemu linux" i klikamy "OK".
Po ponownych uruchomieniu komputera, WSL zostanie zainstalowany. 
Następnie otwieramy Microsoft Store, wyszukujemy w nim "ubuntu", wybieramy pierwszą pozycję i instalujemy go.
 Burpem można posłużyć się [instrucją z laboratorium](https://github.com/djuszka/BAWiM_lab_2021/blob/main/BAWiM_lab2.md#user-content-zadanie-2-konfiguracja-przeglądarki "instrucja z laboratorium") 

##### Polecenie
#####  Atak stored XSS

Zadanie polega na przeprowadzeniu ataku stored XSS, który umożliwi nam zalogowanie się na cudze konto bez loginu i hasła. W tym zadaniu będziemy używać dziurawej aplikacji DVWA. Należy w niej dodać odpowiedni wpis w zakładce XSS (Stored), który wyśle ciasteczka na serwer, który będzie nasłuchiwał. Serwer należy uruchomić na WSL-u, wpisując następującą komendę ”nc -lvp [port]” gdzie [port] to numer portu, na którym będziemy nasłuchiwali. Należy sprawdzić, na jakim poziomie zabezpieczeń możliwy jest atak. W odpowiedzi należy podać użyty kod oraz screen potwierdzający autentyczność rozwiązania.

####Zadanie 4


##### Polecenie
#####  Atak stored XSS

Przeprowadź atak stored XSS na aplikacji DVWA. Dodaj wpis który, umożliwi przesyłanie danych wpisanych, przez innego użytkownika, w formularzu (Name, Message) na nasz nasłuchujący serwer stworzony tak jak w poprzednim zadaniu. W odpowiedzi należy podać użyty kod oraz screen potwierdzający autentyczność rozwiązania.

