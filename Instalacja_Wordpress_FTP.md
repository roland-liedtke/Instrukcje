# Instalacja WordPress przez FTP ( File Transfer Protocol )

## 1. Pierwsza instalacja

<details>
  <summary>
    Wybierz klienta FTP
  </summary>
  <ul>
    <li> FileZilla - MacOS </li>
    <li> WinSCP - Windows </li>
  </ul>
</details>

<details>
  <summary>
    Uzyskaj dane do FTP
  </summary>
  <ul>
    <li> host </li>
    <li> login </li>
    <li> hasło </li>
    <li> protokół i port (najczęściej FTP / 21) </li>
  </ul>
</details>

<details>
  <summary>
    Pobierz pliki WordPress
  </summary>
  <ul>
    <li> ( https://pl.wordpress.org/download/ ) </li>
  </ul>
</details>

<details>
  <summary>
    Rozpakuj zip lokalnie i wrzuć pliki na serwer
  </summary>
  <ul>
    <li> Wrzuć zawartość katalogu wordpress do głównego katalogu ( example.pl ), lub podkatalogu ( example.pl/wordpress ). </li>
  </ul>
</details>  

<details>
  <summary>
    Utwórz bazę danych w panelu hostingu
  </summary>
  <ul>
    <li> nazwa bazy </li>
    <li> nazwa użytkownika </li>
    <li> hasło </li>
    <strong>UWAGA:</strong> Pamiętaj by dać jakieś mało oczywiste hasło i nazwę użytkownika  
  </ul>
</details>

## 2. Konfiguracja wp-config.php

<details>
  <summary>
    Znajdź wp-config-sample.php i zamień nazwę na wp-config.php.
  </summary>
  <ul>
    <li> Otwieramy plik w edytorze tekstowym i wpisujemy to co udało się stworzyć w panelu hostingowym tworząc bazę danych. </li>
    ( name, user, password, host, charset )
  </ul>
</details>

<details>
  <summary>
    Wygeneruj własne klucze zabezpieczające
  </summary>
  <ul>
    <li> Generujemy własne klucze zabezpieczające dane przechowywane w ciasteczkach. </li>
    ( Własne klucze można wygenerować tutaj: https://api.wordpress.org/secret-key/1.1/salt/ )
  </ul>
</details> 

<details>
  <summary>
    Włącz tryb debugowania
  </summary>
  <ul>
    <li> To absolutna podstawa. W trybie debugowania wyświetlane są wszystkie możliwe komunikaty o błędach – łatwo więc wyłapać wszelkie niedociągnięcia i      pomyłki. Aby włączyć ten tryb należy w pliku wp-config.php zmienić następującą linię 
    <pre>
    define('WP_DEBUG', true);</pre>
    </li>
    <li> Po zakończeniu prac nad stroną należy bezwzględnie wyłączyć tryb debugowania. </li>
  </ul>
</details> 

<details>
  <summary>
    Zmień prefiks tabel
  </summary>
  <ul>
    <li> Zmień prefiks w pliku konfiguracyjnym wp-config.php z 'wp_' na coś innego ( $table_prefix = 'wp_'; ).</li>
    <li> Zmień prefiks tabel bazy danych w phpMyAdmin. </li>
    <li> Zmień wartości wybranych opcji w tabeli bazy danych ( wp_options ):
      <ul>
        <li> wp_user_roles </li>
        <li> wp_user_roles </li>
      </ul>
    </li>
    <li> Zmień wartości wybranych opcji w tabeli bazy danych ( wp_usermeta ):
      <ul>
        <li> wp_capabilities </li>
        <li> wp_user_level </li>
        <li> wp_user-settings </li>
        <li> wp_dashboard_quick_press_last_post_id </li>
        <li> wp_user-settings-time </li>
      </ul>
    </li>
  </p>
</details> 


## 3. Dodatkowe Zabezpieczenia

<details>
  <summary>
    Zainstaluj certyfikat SSL
  </summary>
  <p>
    UZUPEŁNIJ
  </p>
</details>

<details>
  <summary>
    Przenieś ustawienia bazy danych do oddzielnego pliku
  </summary>
  <ul>
    <li> Szukamy poniższego fragmentu i kopiujemy do innego pliku – przykładowo 'wp-config-data.php': </li>
    <pre>
    define('DB_NAME', 'moja_baza');
    define('DB_USER', 'moj_user');
    define('DB_PASSWORD', 'moje_haslo');
    define('DB_HOST', 'moj_host');
    define('DB_CHARSET', 'utf8');
    define('DB_COLLATE', '');</pre>
    <li> Następnie w pliku wp-config.php dodajemy: </li>
    <pre>
    require_once "wp-config-data.php";</pre>
  </ul>
</details> 

<details>
  <summary>
    Usuń informacje o wersji wordpressa
  </summary>
  <ul>
    <li> W pliku functions.php dodajemy fragment: </li>
    <pre>
    function remove_version_info() {
    return '';
    } 
    add_filter('the_generator', 'remove_version_info');
    remove_action('wp_head', 'wp_generator');</pre>
  </ul>
</details>

## 4. Na koniec

<details>
  <summary>
    Wyłącz tryb debugowania i ukryj błędy na stronie
  </summary>
  <ul>
    <li> Po zakończeniu prac nad stroną należy bezwzględnie wyłączyć tryb debugowania. </li>
      <pre>
      define('WP_DEBUG', false);
      if ( ! WP_DEBUG ) {
      ini_set('display_errors', 0);
      }
      </pre>
  </ul>
</details> 

<details>
  <summary>
    Wyłącz edycję plików bezpośrednio przez panel admina.
  </summary>
  <ul>
    <li> Wyłączamy możliwość edycji plików motywu i wtyczek bezpośrednio przez panel WordPress. W pliku wp-config.php dopisując do niego fragment: </li>
    <pre>
    define('DISALLOW_FILE_EDIT', true);
    </pre>
  </ul>
</details>

<details>
  <summary>
    Zablokuj dostęp do pliku wp-login.php
  </summary>
  <ul>
    <li> Najprostsza metoda zabezpieczenia tegoż pliku to dodanie w '.htaccess' takie cuda: </li>
    <pre>
    <IfModule mod_rewrite.c>
    RewriteEngine On
    RewriteCond %{REQUEST_METHOD} POST
    RewriteCond %{HTTP_REFERER} !^http://(.*)?.nasza-domena.pl [NC]
    RewriteCond %{REQUEST_URI} ^/wp-login\.php(.*)$
    RewriteRule ^(.*)$ - [R=403,L]
    </IfModule>
    </pre>
  </ul>
</details>

<details>
  <summary>
    Zablokuj dostęp do pliku xmlrpc.php
  </summary>
  <ul>
    <li> Plik ten jest drugim w kolejności, który jest najczęściej atakowany (pierwszy to wp-login.php). Jeśli nie korzysta się z interfejsu XML-RPC to można go całkowicie zablokować dodając w '.htaccess': </li>
    <pre>
    <files xmlrpc.php>
    order deny,allow
    deny from all
    </files>
    </pre>
  </ul>
</details>

<details>
  <summary>
    Zablokuj dostęp do kolejnych plików
  </summary>
  <ul>
    <li> Są pliki, do których NIKT NIGDY nie powinien mieć dostępu. Należy wpisać w pliku '.htaccess': </li>
    <pre>
    <FilesMatch "wp-config.*\.php|\.htaccess|readme\.html">
    Order allow,deny
    Deny from all
    </FilesMatch>
    </pre>
  </ul>
</details>

<details>
  <summary>
    Włącz zabezpieczenie dla wp-includes
  </summary>
  <ul>
    <li> W katalogu wp-includes tworzymy plik '.htaccess' i dodajemy do niego: </li>
    <pre>
    <FilesMatch "\.(?i:php)$">
    Order allow,deny
    Deny from all
    </FilesMatch>
    <Files wp-tinymce.php>
    Allow from all
    </Files>
    <Files ms-files.php>
    Allow from all
    </Files>
    </pre>
  </ul>
</details>

<details>
  <summary>
    Sprawdź uprawnienia do katalogów
  </summary>
  <ul>
    <li> Standardowy schemat uprawnień wygląda mniej więcej tak: </li>
    <pre>katalog główny / – 644
/wp-admin – 644
/wp-includes – 644
/wp-content/uploads – 755
Plik `.htaccess` powinien mieć uprawnienia 644.
  </ul>
</details>

<details>
  <summary>
    Wyłączamy możliwość rejestracji przypadkowych osobników
  </summary>
  <ul>
    <li> ( Ustawienia / Ogólne / Członkostwo ) </li>
  </ul>
</details>

### EXTRA:
- Aktualizujmy motywy, wtyczki i wordpressa <br>
`UWAGA:` przed przystąpieniem do aktualizacji warto sobie zrobić backup strony
- Usuwajmy nieużywane i zbędne wtyczki oraz motywy
- Wykonuj codziennie BACKUPY. Są one ważne nie tylko wtedy, gdy coś psujecie. Warto je robić na bieżąco by w razie wstrzyknięcia złośliwego kodu lub innego ustrojstwa mieć z czego przywrócić stronę.
- Po zainstalowaniu WP przejdź do sekcji USTAWIENIA – OGÓLNE zmień SLOGAN, a w sekcji BEZPOŚREDNIE ODNOŚNIKI np. na nazwa wpisu lub stwórz własny format – na pewno nie zaznaczaj opcji PROSTY
- Wtyczki / motywy najlepiej testuj poza docelową stroną, bo nawet jak zostaną usunięte to zostawiają po sobie ślady chociażby w bazie danych. 
- Jeśli wgrywasz demo motywu sprawdź wtyczki czy wszystkie, które się z nim zainstalowały na pewno są Ci potrzebne. Usuń wszystkie, które zbędne. 
- Przy instalacji demo zaciągane są też podstrony, wpisy, produkty oraz np. portfolio czy jeszcze inne typy wpisów – pamiętaj by przed puszczeniem w świat strony wszystkie rzeczy z demo pousuwać by nie zostały zaindeksowane.
- Pamiętaj o polityce prywatności, informacji o ciasteczkach i regulaminie jeśli masz sklep oraz ewentualnie innych prawnych dokumentach, których wymaga Twój projekt np. regulamin programu partnerskiego, jeśli takowy jest u Ciebie. Pamiętaj także, by przy formularzach kontaktu, newslettera, etc dodać checkbox ze zgodą na przetwarzanie danych osobowych.
- Dodaj do strony reCaptchę by uniknąć spamu prz formularzach np. kontaktowym.
