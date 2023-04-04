# Instalacja WordPress przez FTP ( File Transfer Protocol )

### 1. Pierwsza instalacja

<details>
  <summary>
    Wybierz klienta FTP
  </summary>
  <p>
    (np. FileZilla - MacOS, WinSCP - Windows)
  </p>
</details>

<details>
  <summary>
    Uzyskaj dane do FTP
  </summary>
  <p>
    (host, login, hasło, protokół i port (dwa ostatnie to najczęściej FTP / 21)
  </p>
</details>

<details>
  <summary>
    Pobierz pliki WordPress
  </summary>
  <p>
    ( https://pl.wordpress.org/download/ )
  </p>
</details>

<details>
  <summary>
    Rozpakuj zip lokalnie i wrzuć pliki na serwer
  </summary>
  <p>
    Wrzuć zawartość katalogu wordpress do głównego katalogu (example.pl), lub podkatalogu (example.pl/wordpress).
  </p>
</details>  

<details>
  <summary>
    Utwórz bazę danych w panelu hostingu
  </summary>
  <p>
    ( nazwa bazy, nazwa użytkownika, hasło ) <br>
    <strong>UWAGA:</strong> Pamiętaj by dać jakieś mało oczywiste hasło i nazwę użytkownika  </p>
</details>  

### 2. Konfiguracja wp-config.php

<details>
  <summary>
    Znajdź wp-config-sample.php i zamień nazwę na wp-config.php.
  </summary>
  <p>
    Otwieramy plik w edytorze tekstowym i wpisujemy to co udało się stworzyć w panelu hostingowym tworząc bazę danych.<br>
    ( name, user, password, host, charset )
  </p>
</details> 

<details>
  <summary>
    Włącz tryb debugowania
  </summary>
  <p>
    To absolutna podstawa. W trybie debugowania wyświetlane są wszystkie możliwe komunikaty o błędach – łatwo więc wyłapać wszelkie niedociągnięcia i pomyłki. Aby włączyć ten tryb należy w pliku wp-config.php zmienić następującą linię
<pre>define('WP_DEBUG', true);</pre>
Po zakończeniu prac nad stroną należy bezwzględnie wyłączyć tryb debugowania.
  </p>
</details> 

<details>
  <summary>
    Zmień prefiks tabel
  </summary>
  <p>
    - Zmień prefiks w pliku konfiguracyjnym wp-config.php z 'wp_' na coś innego ( $table_prefix = 'wp_'; ).<br>
    - Zmień prefiks tabel bazy danych w phpMyAdmin.<br>
    - Zmień wartości wybranych opcji w tabeli bazy danych ( wp_options ):<br>
    -- `wp_user_roles`,
    -- `wp_user_roles`,
    - Zmień wartości wybranych opcji w tabeli bazy danych ( wp_usermeta ):<br>
    -- `wp_capabilities`,
    -- `wp_user_level`,
    -- `wp_user-settings`,
    -- `wp_dashboard_quick_press_last_post_id`,
    -- `wp_user-settings-time`.
  </p>
</details> 

<details>
  <summary>
    Wygeneruj własne klucze zabezpieczające
  </summary>
  <p>
    Generujemy własne klucze zabezpieczające dane przechowywane w ciasteczkach. <br>
    ( Własne klucze można wygenerować tutaj: https://api.wordpress.org/secret-key/1.1/salt/ )
  </p>
</details> 

<details>
  <summary>
    Ukryj błędy na stronie
  </summary>
  <p>
    Ukrywamy błędy ( w pliku `wp-config.php` ). Szukamy teraz:
  <pre>define('WP_DEBUG', false); </pre>
  i zamieniamy ten fragment na:
  <pre>define('WP_DEBUG', false);
  if ( ! WP_DEBUG ) {
  ini_set('display_errors', 0);
  }
  </pre>
  </p>
</details> 


### 7. Dodatkowe Zabezpieczenia

1. Instalujemy certyfikat SSL

4. Przenosimy dane bazy. Szukamy poniższego fragmentu i kopiujemy do innego pliku – przykładowo `wp-config-data.php`
<pre>define('DB_NAME', 'moja_baza');
define('DB_USER', 'moj_user');
define('DB_PASSWORD', 'moje_haslo');
define('DB_HOST', 'moj_host');
define('DB_CHARSET', 'utf8');
define('DB_COLLATE', ''); </pre>

5. Następnie w pliku `wp-config.php` dodajemy:
<pre>require_once "wp-config-data.php"; </pre>

6. Wyłączamy możliwość edycji plików motywu i wtyczek bezpośrednio przez panel WordPress. W pliku `wp-config.php` dopisując do niego fragment:
<pre>define('DISALLOW_FILE_EDIT', true); </pre>

7. Usuwamy informacje o wersji wordpressa. W pliku `functions.php` dodajemy fragment:
<pre>function remove_version_info() { return ''; } add_filter('the_generator', 'remove_version_info'); remove_action('wp_head', 'wp_generator');</pre>

8. Blokujmy dostęp do pliku `wp-login.php`
Najprostsza metoda zabezpieczenia tegoż pliku to dodanie w `.htaccess` takie cuda:
```
<IfModule mod_rewrite.c>
RewriteEngine On
RewriteCond %{REQUEST_METHOD} POST
RewriteCond %{HTTP_REFERER} !^http://(.*)?.nasza-domena.pl [NC]
RewriteCond %{REQUEST_URI} ^/wp-login\.php(.*)$
RewriteRule ^(.*)$ - [R=403,L]
</IfModule>
```

9. Blokujemy dostęp do pliku `xmlrpc.php`
Plik ten jest drugim w kolejności, który jest najczęściej atakowany (pierwszy to wp-login.php). Jeśli nie korzysta się z interfejsu XML-RPC to można go całkowicie zablokować dodając w `.htaccess`:
```
<files xmlrpc.php>
order deny,allow
deny from all
</files>
```

10. Blokujemy dostęp do kolejnych plików
Są pliki, do których NIKT NIGDY nie powinien mieć dostępu. Należy wpisać w pliku `.htaccess`:
```
<FilesMatch "wp-config.*\.php|\.htaccess|readme\.html">
Order allow,deny
Deny from all
</FilesMatch>
```
Plik `.htaccess` powinien mieć uprawnienia 644.

11. Włączamy zabezpieczenia dla `wp-includes`
W katalogu `wp-includes` tworzymy plik `.htaccess` i dodajemy do niego:
```
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
```

12. Sprawdzamy uprawnienia do katalogów
Jeśli nic nie grzebaliście w uprawnieniach to nie powinno być tutaj nic do zrobienia. Standardowy schemat uprawnień wygląda mniej więcej tak:
<pre>katalog główny / – 644
/wp-admin – 644
/wp-includes – 644
/wp-content/uploads – 755</pre>

13. Wyłączamy możliwość rejestracji przypadkowych osobników ( Ustawienia / Ogólne / Członkostwo )

### 8. Instalujemy WP
`UWAGA:` Jeśli macie podpięty na hostingu SSL to warto przy instalacji podać adres z `https://`

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
