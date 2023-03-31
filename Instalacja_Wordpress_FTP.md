# Instalacja WordPress przez FTP ( File Transfer Protocol )

### 1. Potrzebny będzie nam klient FTP
- (np. FileZilla - MacOS, WinSCP - Windows)
  
### 2. Ogarniamy dane do FTP
- (host, login, hasło, protokół i port (dwa ostatnie to najczęściej FTP / 21)
  
### 3. Pobieramy pliki WordPress
- ( https://pl.wordpress.org/download/ )
  
### 4. Rozpakowujemy zip lokalnie i wrzucamy pliki na serwer
  
### 5. Tworzymy bazę danych w panelu hostingu
- ( nazwa bazy, nazwa użytkownika, hasło ) <br>
`UWAGA:` Pamiętaj by dać jakieś mało oczywiste hasło i nazwę użytkownika
  
### 6. Uzupełniamy WP-CONFIG
1. W plikach, które wgraliśmy szukamy `wp-config-sample.php` i zmieniamy mu nazwę na `wp-config.php`. Następnie otwieramy plik w edytorze tekstowym i w miejscu na dane bazy wpisujemy to co udało nam się wyczarować w panelu hostingowym.

2. Zmieniamy prefiks w pliku konfiguracyjnym CMS `wp-config.php` na serwerze FTP z `wp_` na coś innego ( `$table_prefix = 'wp_';` ).

3. Zmieniamy prefiks tabel bazy danych w phpMyAdmin.

4. Zmieniamy wartości wybranych opcji w tabeli bazy danych ( `wp_options` ):
- `wp_user_roles`,

5. Zmieniamy wartości wybranych opcji w tabeli bazy danych ( `wp_usermeta` ):
- `wp_capabilities`,
- `wp_user_level`,
- `wp_user-settings`,
- `wp_dashboard_quick_press_last_post_id`,
- `wp_user-settings-time`.

### 7. Dodatkowe Zabezpieczenia

1. Instalujemy certyfikat SSL

2. Generujemy własne klucze zabezpieczające dane przechowywane w ciasteczkach ( Własne klucze można wygenerować tutaj: https://api.wordpress.org/secret-key/1.1/salt/ )

3. Ukrywamy błędy ( w pliku `wp-config.php` ). Szukamy teraz:
<pre>define('WP_DEBUG', false); </pre>
i zamieniamy ten fragment na:
<pre>define('WP_DEBUG', false);
if ( ! WP_DEBUG ) {
ini_set('display_errors', 0);
} </pre>

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
- Nie używamy loginu ADMIN. Stosujmy mniej oczywistą nazwę użytkownika, który ma uprawnienia administratora 
- Stosujmy skomplikowane hasła. Nie dawajcie tego samego hasła do panelu WordPress, do bazy danych, jako hasło do FTP lub innego powiązanego z Waszą witryną miejsca. Nie zapisujcie haseł w przeglądarce
- Aktualizujmy motywy, wtyczki i wordpressa <br>
`UWAGA:` przed przystąpieniem do aktualizacji warto sobie zrobić backup strony
- Usuwajmy nieużywane i zbędne wtyczki oraz motywy
- Korzystajmy wyłącznie z zaufanych źródeł wtyczek i motywów
- Wykonuj codziennie BACKUPY Backupy są ważne nie tylko wtedy, gdy coś psujecie. Warto je robić na bieżąco by w razie wstrzyknięcia złośliwego kodu lub innego ustrojstwa mieć z czego przywrócić stronę
- Po zainstalowaniu WP przejdź do sekcji USTAWIENIA – OGÓLNE zmień SLOGAN, a w sekcji BEZPOŚREDNIE ODNOŚNIKI np. na nazwa wpisu lub stwórz własny format – na pewno nie zaznaczaj opcji PROSTY
- Wtyczki / motywy najlepiej testuj poza docelową stroną, bo nawet jak zostaną usunięte to zostawiają po sobie ślady chociażby w bazie danych. 
- Jeśli wgrywasz demo motywu sprawdź wtyczki czy wszystkie, które się z nim zainstalowały na pewno są Ci potrzebne. Usuń wszystkie, które zbędne. 
- Przy instalacji demo zaciągane są też podstrony, wpisy, produkty oraz np. portfolio czy jeszcze inne typy wpisów – pamiętaj by przed puszczeniem w świat strony wszystkie rzeczy z demo pousuwać by nie zostały zaindeksowane.
- Pamiętaj o polityce prywatności, informacji o ciasteczkach i regulaminie jeśli masz sklep oraz ewentualnie innych prawnych dokumentach, których wymaga Twój projekt np. regulamin programu partnerskiego, jeśli takowy jest u Ciebie. Pamiętaj także, by przy formularzach kontaktu, newslettera, etc dodać checkbox ze zgodą na przetwarzanie danych osobowych.
- Dodaj do strony reCaptchę by uniknąć spamu prz formularzach np. kontaktowym.
- Pamiętaj o dodaniu do strony Google Analytics, Google Search Console oraz ewentualnie piksela Facebooka – w końcu przyjdzie taki moment, że będziesz chcieć sprawdzić statystyki czy zacząć reklamę na FB.
