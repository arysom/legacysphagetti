Posiadasz komputer, wiedzę na temat internetu i chciałbyś zacząć robić strony. Html, może nawet PHP już nie jest ci tak całkiem obce, ale chciałbyś zacząć tworzyć szybciej. Od tego masz właśnie Codeigniter. Na stronie polskiej społeczności CI jest wpis dotyczący początkowej konfiguracji frameworka, jednak w tym miejscu zajmiemy się wydarzeniami, które mają miejsce przedtem.

<!-- pagebreak -->

##Potrzebne programy

Jeśli chcesz zająć się tworzeniem stron/aplikacji powinieneś posiadać w komputerze odpowiednie oprogramowanie, a także serwer zdalny, żeby ktoś mógł obejrzeć na żywo twój produkt. Oto lista potrzebnych rzeczy:

1. Edytor tekstu.
2. Przeglądarka.
3. Serwer lokalny.
4. Program do wysyłania danych.
5. Serwer zdalny.

Niewiele jest pozycji, jednak zawierają one pewną liczbę zagadnień do omówienia. Kolejność jest nieprzypadkowa, od wyprodukowania strony na własnym komputerze, do wysłania jej finalnej(przynajmniej działającej) wersji w sieć. Poniższy artykuł odnosi się do środowiska Windows. Wybrane sposoby i programy niekoniecznie muszą być najlepszym rozwiązaniem, a na pewno nie są jedynym.

##Edytor tekstu

Tworzenie stron to praca z tekstem. Trzeba mieć świadomość, z czego zbudowana jest strona, znać podstawową strukturę, i wiedzieć za co odpowiedzialne są podstawowe tagi. Aby pisanie było przyjemną czynnością warto oswoić się z jakimś edytorem tekstów, dowiedzieć się, jak poruszać się między plikami projektu i zapoznać się ze skrótami klawiszowymi, a także poszukać funkcji autouzupełniania kodu.

Przykładowym przedstawicielem "lekkich" edytorów jest notepad++, który pod płaszczykiem minimalnego interfejsu jest pełnoprawnym środowiskiem developerskim. Inne programy to np. ecplise i netbeans, oraz vim.

Jeśli już pracujesz z codeigniterem - edytory wizualne niekoniecznie będą się nadawały.


##Przeglądarka

Wszystko co zrobimy, będziemy wyświetlać w przeglądarce. Jest ich wiele. Na dodatek nasze strony nie zawsze w każdej z nich wyglądają tak samo. Główni gracze w tej kategorii to : Firefox, Chrome oraz Internet explorer. 

Warto dozbroić swoją przeglądarkę do 

##Serwer lokalny

Na tym etapie możesz zainstalować środowisko developerskie, które pozwoli na działanie aplikacji w php na Twoim komputerze. Jednym z programów zawierających wszystko, co potrzebne na start, jest [xampp](http://apachefriends.org). Zawiera on w pakiecie serwer apache, język PHP i serwer bazy danych - MySql, oraz program phpMyAdmin, który udostępnia interfejs do tworzenia potrzebnych struktur w przyjazny, wizualny sposób. Istnieje również wiele innych programów, które oferują podobne lub trochę inne możliwości niż xampp: zwamp, uniserwer, wamp, czy polski krasnal.

Po przejściu procesu instalacji możemy wpisać w przeglądarce adres 'localhost' i zobaczyć zawartość katalogu htdocs znajdującego się w ścieżce programu xampp. Czasami to miejsce może znajdować się dość głęboko w strukturze katalogów, np gdy instalujesz program na pulpicie (c:\users\gosc\desktop\xampp\htdocs). Jednak katalog stron lokalnych może znajdować się w innym miejscu. Wszystko zależy od konfiguracji pliku httpd-vhosts.conf. Ale po kolei.

Do uruchomienia strony PHP potrzebna będzie edycja dwóch plików.  Wspomnianego httpd-vhosts.conf oraz hosts(po prostu hosts, bez rozszerzenia), który znajduje się zazwyczaj w c:\windows\system32\drivers\etc. 

###hosts

To plik odpowiedzialny za przekierowanie żądań stron na adres znajdujący się w komputerze użytkownika. W przypadku gdy pracujemy nad stroną lokalnie, czyli na naszym sprzęcie, jest to kluczowa sprawa. Zazwyczaj jego zawartość wygląda mniej więcej tak:

	# Komentarz do pliku hosts (np. opis budowy pliku)
	127.0.0.1  localhost loopback
	::1        localhost


c.d.n.
