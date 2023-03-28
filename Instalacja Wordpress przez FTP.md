# Instalacja WordPress przez FTP ( File Transfer Protocol )

### 1. Potrzebny będzie nam klient FTP
- (np. FileZilla)
  
### 2. Ogarniamy dane do FTP
- (host, login, hasło, protokół i port (dwa ostatnie to najczęściej FTP / 21)
  
### 3. Pobieramy pliki WordPress
- ( https://pl.wordpress.org/download/ )
  
### 4. Rozpakowujemy zip lokalnie i wrzucamy pliki na serwer
  
### 5. Tworzymy bazę danych w panelu hostingu
- ( nazwa bazy, nazwa użytkownika, hasło ) <br>
`UWAGA:` Pamiętaj by dać jakieś mało oczywiste hasło i nazwę użytkownika
  
### 6. Uzupełniamy dane w pliku wp-config
- W plikach, które wgraliśmy szukamy `wp-config-sample.php` i zmieniamy mu nazwę `na wp-config.php`. Następnie otwieramy plik w edytorze tekstowym i w miejscu na dane bazy wpisujemy to co udało nam się wyczarować w panelu hostingowym
- Zmieniamy prefix bazy danych z `wp_` na coś innego
- Generujemy własne klucze zabezpieczające dane przechowywane w ciasteczkach ( Własne klucze można wygenerować tutaj: https://api.wordpress.org/secret-key/1.1/salt/ )
- Przenosimy dane bazy. Szukamy fragmentu:
<pre>define('DB_NAME', 'moja_baza');
define('DB_USER', 'moj_user');
define('DB_PASSWORD', 'moje_haslo');
define('DB_HOST', 'moj_host');
define('DB_CHARSET', 'utf8');
define('DB_COLLATE', ''); </pre>
i kopiujemy je do innego pliku – przykładowo `wp-config-data.php` a następnie w pliku `wp-config.php` dodajemy:
<pre>require_once "wp-config-data.php"; </pre>
- Ukrywamy błędy ( w pliku `wp-config.php` ). Szukamy teraz:
<pre>define('WP_DEBUG', false); </pre>
i zamieniamy ten fragment na:
<pre>define('WP_DEBUG', false);
if ( ! WP_DEBUG ) {
ini_set('display_errors', 0);
} </pre>
- Wyłączamy możliwość edycji plików motywu i wtyczek bezpośrednio przez panel WordPress. W pliku `wp-config.php` dopisując do niego fragment:
<pre>define('DISALLOW_FILE_EDIT', true); </pre>
- Nie używamy loginu ADMIN. Stosujmy mniej oczywistą nazwę użytkownika, który ma uprawnienia administratora
- Stosujmy skomplikowane hasła. Nie dawajcie tego samego hasła do panelu WordPress, do bazy danych, jako hasło do FTP lub innego powiązanego z Waszą witryną miejsca. Nie zapisujcie haseł w przeglądarce
- Aktualizujmy motywy, wtyczki i wordpressa <br>
`UWAGA:` przed przystąpieniem do aktualizacji warto sobie zrobić backup strony
- Usuwajmy nieużywane i zbędne wtyczki oraz motywy
- Korzystajmy wyłącznie z zaufanych źródeł wtyczek i motywów
- Wyłączamy możliwość rejestracji przypadkowych osobników ( Ustawienia / Ogólne / Członkostwo )
- Instalujemy certyfikat SSL
- Usuwamy informacje o wersji wordpressa. W pliku `functions.php` dodajemy fragment:
<pre>function remove_version_info() { return ''; } add_filter('the_generator', 'remove_version_info'); remove_action('wp_head', 'wp_generator');</pre>
- Blokujmy dostęp do pliku `wp-login.php`
Najprostsza metoda zabezpieczenia tegoż pliku to dodanie w `.htaccess` takie cuda:
        <code><IfModule mod_rewrite.c>
RewriteEngine On
RewriteCond %{REQUEST_METHOD} POST
RewriteCond %{HTTP_REFERER} !^http://(.*)?.nasza-domena.pl [NC]
RewriteCond %{REQUEST_URI} ^/wp-login\.php(.*)$
RewriteRule ^(.*)$ - [R=403,L]
          </IfModule></code>
- Blokujemy dostęp do pliku `xmlrpc.php`
Plik ten jest drugim w kolejności, który jest najczęściej atakowany (pierwszy to wp-login.php). Jeśli nie korzysta się z interfejsu XML-RPC to można go całkowicie zablokować dodając w `.htaccess`:
<pre>
<files xmlrpc.php>
order deny,allow
deny from all
      </files> </pre>
- Blokujemy dostęp do kolejnych plików
Są pliki, do których NIKT NIGDY nie powinien mieć dostępu. Należy wpisać w pliku `.htaccess`:
<pre>
<FilesMatch "wp-config.*\.php|\.htaccess|readme\.html">
   Order allow,deny
   Deny from all
      </FilesMatch> </pre>
- Włączamy zabezpieczenia dla `wp-includes`
W katalogu `wp-includes` tworzymy plik `.htaccess` i dodajemy do niego:
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
      </Files> </pre>
- Sprawdzamy uprawnienia do katalogów
Jeśli nic nie grzebaliście w uprawnieniach to nie powinno być tutaj nic do zrobienia. Standardowy schemat uprawnień wygląda mniej więcej tak:
> katalog główny / – 644 <br>
> /wp-admin – 644 <br>
> /wp-includes – 644 <br>
> /wp-content/uploads – 755
- Wykonuj codziennie BACKUPY
Backupy są ważne nie tylko wtedy, gdy coś psujecie. Warto je robić na bieżąco by w razie wstrzyknięcia złośliwego kodu lub innego ustrojstwa mieć z czego przywrócić stronę

### 7. Instalujemy WP
`UWAGA:` Jeśli macie podpięty na hostingu SSL to warto przy instalacji podać adres z `https://`
