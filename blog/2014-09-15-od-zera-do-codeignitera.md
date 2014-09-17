Posiadasz komputer, wiedzę na temat internetu i chciałbyś zacząć robić strony. Html, może nawet PHP już nie jest ci tak całkiem obce, ale chciałbyś zacząć tworzyć szybciej. Od tego masz właśnie Codeigniter. Na stronie polskiej społeczności CI jest [wpis dotyczący początkowej konfiguracji frameworka](http://www.codeigniter.org.pl/konfiguracja-podstawowa/), jednak w tym miejscu zajmiemy się wydarzeniami, które mają miejsce nieco przedtem.

<!-- pagebreak -->

##Serwer lokalny

Aby wystartować z Codeigniterem należy zainstalować środowisko developerskie, które pozwoli na działanie aplikacji w php na Twoim komputerze. Jednym z programów zawierających wszystko, co potrzebne na start, jest [xampp](http://apachefriends.org). Zawiera on w pakiecie serwer apache, język PHP i serwer bazy danych - MySql, oraz program phpMyAdmin, który udostępnia interfejs do tworzenia potrzebnych struktur w przyjazny, wizualny sposób. Istnieje również wiele innych programów, które oferują podobne lub trochę inne możliwości niż xampp: zwamp, uniserwer, wamp, czy polski krasnal.

Po przejściu procesu instalacji, należy uruchomić plik setup_xampp.bat z katalogu xamppa, który zarejestruje w systemie swoje zmienne. Możemy wtedy wpisać w przeglądarce adres 'localhost'(phpmyadmin znajduje się pod localhost/phpmyadmin) i zobaczyć zawartość katalogu htdocs znajdującego się w ścieżce programu xampp. Czasami to miejsce może znajdować się dość głęboko w strukturze katalogów, np gdy instalujesz program na pulpicie (c:\users\gosc\desktop\xampp\htdocs). Jednak katalog stron lokalnych może znajdować się w innym miejscu. Wszystko zależy od konfiguracji pliku httpd-vhosts.conf. Ale po kolei.

Do uruchomienia strony PHP potrzebna będzie edycja dwóch plików.  Wspomnianego httpd-vhosts.conf oraz hosts(po prostu hosts, bez rozszerzenia), który znajduje się zazwyczaj w c:\windows\system32\drivers\etc. 

###hosts

To plik odpowiedzialny za przekierowanie żądań stron na adres znajdujący się w komputerze użytkownika. W przypadku gdy pracujemy nad stroną lokalnie, czyli na naszym sprzęcie, jest to kluczowa sprawa. Zazwyczaj jego zawartość wygląda mniej więcej tak:

	# Komentarz do pliku hosts (np. opis budowy pliku)
	127.0.0.1  localhost loopback
	::1        localhost

Następnym krokiem będzie dodanie naszego lokalnego adresu. Niekoniecznie musi to być adres taki sam jak strona, która ma się znaleźć w internecie. Dodajmy na końcu wymyślony adres lub wiele adresów. Dla rozróżnienia ze stronami z internetu proponuję dodać końcówkę .local.

	# Komentarz do pliku hosts (np. opis budowy pliku)
	127.0.0.1  localhost loopback
	::1        localhost
    127.0.0.1 cibase.local  #ci base od codeigniter base
    127.0.0.1 cibase2.local #druga strona na ci
    127.0.0.5 shopping.local #jakas inna aplikacja
 
W ostatniej linijce dla odmiany modyfikujemy ostatnią cyfrę adresu, żeby odróżnić adresy pod względem ip, takie postępowanie przydaje się np. gdy potrzebny jest adres zwrotny w aplikacji wykorzystującej płatności online. Warto też pamiętać, że jako plik systemowy, należy dokonywać jego edycji w trybie administratora, czy to klikając na ikonkę programu do edycji tekstu i uruchamiając go jako administrator, czy logując się na konto administratora. Następnie modyfikujemy plik vhosts.

###vhosts

Ten plik pokazuje położenie katalogów z wirtualnymi hostami, czyli naszą stroną. Jak już wspomnieliśmy, można zdecydować, że nasze strony będę leżały np w katalogu d:/strony. Sam plik vhosts(pełna nazwa httpd-vhosts.conf) w przypadku xamppa znajduje się w /ścieżka do xampp/apache/conf/extra/. Edytujemy go dowolnym edytorem tekstu. Przykładowa zawartość:

	<VirtualHost 127.0.0.26:80>
	DocumentRoot "D:/strony/cibase"
	ServerName cibase.local
	<Directory "D:/strony/cibase">
		Options All
		AllowOverride All
		Require all granted 
	</Directory>
	</VirtualHost>

Mnożymy powyższą dyrektywę dowolną ilość razy i mamy wirtualne serwery dla każdej z naszych stron na komputerze. Czasami potrzebna jest część określająca prawa dostępu do katalogu(<Directory>, w przypadku bardziej restrykcyjnych wersji systemu.

Teraz już tylko założyć katalog zgodnie z wartością DocumentRoot, wrzucić paczkę Codeignitera, rozpakować archiwum, wcisnąć xampp start i wejść do przeglądarki wpisując adres http://cibase.local, a oczom naszym ukaże się znajoma plansza welcome_message z ulubionego frameworka.
