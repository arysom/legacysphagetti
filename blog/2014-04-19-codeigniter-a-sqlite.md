#codeigniter a sqlite

Z pomocą kochającym małe strony z szybkim startem przychodzi sqlite. Nie ma może tylu możliwości co mysql, ale można stworzyć strukturę, sprawdzić działanie i ominąć etap zakładania  bazy danych poprzez interfejs cpanel'u na serwerze. Synchronizacja między stronami lokalną i zdalną może sprowadzać się do skopiowania pliku.

<!-- pagebreak -->
##Ustawienia bazy danych

W codeigniter, żeby skorzystać z sqlite należy wejść do /application/config/database.php i tam od linijki 51ej dokonać następujących zmian:

    $db['default']['hostname'] = 'sqlite:'.APPPATH.'db/blog.sqlite;
    $db['default']['username'] = '';
    $db['default']['password'] = '';
    $db['default']['database'] = '';
    $db['default']['dbdriver'] = 'pdo';

Wcześniej należy utworzyć plik o nazwie np. blog.sqlite w folderze application/db lub miejscu, gdzie będziemy trzymać nasze dane.

W przypadku użycia drivera pdo nie wyświetla nam się błąd w stylu frameworka w ramce i z opisem, tylko zwykły błąd php pdo. Trudniej wtedy zrozumieć własne błędy. W przypadku sqlite codeigniter nie podpowie błędów składni, zamiast tego wyświetli:
>Fatal error: Call to a member function execute() on a non-object in D:\strony\codeigniterbase\system\database\drivers\pdo\pdo_driver.php on line 193

Tak jak mysql ma swojego phpMyadmin albo adminera, tak i sqlite ma swojego managera. Sprawę załatwi np. SQLite Manager, który jest wtyczką do firefoxa. Można w nim stworzyć tabele i sprawdzić zapytanie. Wystarczy połączyć się z bazą danych, czyli w tym przypadku wybrać odpowiedni plik (menu database -> connect database).

##Nasza sesja
Proces tworzenia tabel jest podobny do tego z phpMyadmin, ale składnia sql trochę się różni. Przyjrzyjmy się tym różnicom na podstawie tabeli ci_sessions. W mysql tabela wygląda tak:

    CREATE TABLE IF NOT EXISTS  `ci_sessions` (
    	session_id varchar(40) DEFAULT '0' NOT NULL,
    	ip_address varchar(45) DEFAULT '0' NOT NULL,
    	user_agent varchar(120) NOT NULL,
    	last_activity int(10) unsigned DEFAULT 0 NOT NULL,
    	user_data text NOT NULL,
    PRIMARY KEY (session_id),
    KEY `last_activity_idx` (`last_activity`)
    );

Z kolei w sqlite sprawy mają się następująco:
    
    CREATE TABLE "ci_sessions" (
	"session_id" VARCHAR PRIMARY KEY  NOT NULL DEFAULT 0, 
	"ip_address" VARCHAR NOT NULL  DEFAULT 0, 
	"user_agent" VARCHAR NOT NULL  DEFAULT 0,
	"last_activity" INTEGER NOT NULL  DEFAULT 0, 	
	"user_data" TEXT NOT NULL
     )

Mniej tu szczegółów (nie trzeba uściślać ile znaków posiada typ varchar), mniej typów - nie ma enum, tinyint, text jest tylko text'em, nie ma typów fulltext, mediumtext.

##Blogowe archiwa

Inne są funkcje daty i czasu. Często korzystając z pól typu datetime potrzebujemy np. osobno miesiąca, osobno roku, żeby dla przykładu wyświetlić podsumowanie wpisów w postaci archiwum:

    SELECT 
    	strftime('%Y',created_at) AS YEAR, 
    	strftime('%m',created_at) AS MONTH,
    COUNT(*) AS TOTAL 
    FROM articles
    GROUP BY YEAR, MONTH
    ORDER BY YEAR DESC, MONTH DESC

W mysql wystarczyło MONTH, albo nawet MONTHNAME, zaś w tym przypadku posługujemy się jedną funkcją.

##PDO a to co?

Korzystając z sqlite w codeigniterze używa się PDO, która jest rekomendowana jako podstawowy sterownik baz danych w php. Warto przyjrzeć się temu rozszerzeniu w manualu, żeby lepiej zrozumieć istotę programowania.
