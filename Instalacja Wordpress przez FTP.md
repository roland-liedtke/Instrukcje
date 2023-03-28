# Instalacja WordPress przez FTP ( File Transfer Protocol )

<ol>
  <li> Potrzebny będzie nam klient FTP (np. FileZilla) </li>
  <li> Ogarniamy dane do FTP (host, login, hasło, protokół i port (dwa ostatnie to najczęściej FTP / 21) </li>
  <li> Pobieramy pliki WordPress ( https://pl.wordpress.org/download/ ) </li>
  <li> Rozpakowujemy zip lokalnie i wrzucamy pliki na serwer </li>
  <li> Tworzymy bazę danych w panelu hostingu ( nazwa bazy, nazwa użytkownika, hasło ) <br>
    <strong>UWAGA: </strong> Pamiętaj by dać jakieś mało oczywiste hasło i nazwę użytkownika </li>
<li> Uzupełniamy dane bazy w pliku wp-config. W plikach, które wgraliśmy szukamy wp-config-sample.php i zmieniamy mu nazwę na wp-config.php. Następnie otwieramy plik w edytorze tekstowym i w miejscu na dane bazy wpisujemy to co udało nam się wyczarować w panelu hostingowym
  <ul>
    <li> Zmieniamy prefix bazy danych z wp_ na coś innego </li>
    <li> Generujemy własne klucze zabezpieczające dane przechowywane w ciasteczkach </li>
    <li> Przenosimy dane bazy do osobnego pliku </li>
    <li> Ukrywamy błędy na stronie </li>
    <li> Wyłączamy możliwość edycji plików motywu i wtyczek bezpośrednio przez panel WordPress </li>
    <li> Nie używamy loginu ADMIN. Stosujmy mniej oczywistą nazwę użytkownika, który ma uprawnienia administratora </li>
    <li> Stosujmy skomplikowane hasła. Nie dawajcie tego samego hasła do panelu WordPress, do bazy danych, jako hasło do ftp lub innego powiązanego z Waszą witryną miejsca. Nie zapisujcie haseł w przeglądarce </li> 
    <li> Aktualizujmy motywy, wtyczki i wordpressa <br>
      <strong>UWAGA: </strong> przed przystąpieniem do aktualizacji warto sobie zrobić backup strony </li>
    <li> Usuwajmy nieużywane i zbędne wtyczki oraz motywy </li>
    <li> Korzystajmy wyłącznie z zaufanych źródeł wtyczek i motywów </li>
    <li> Wyłączamy możliwość rejestracji przypadkowych osobników ( Ustawienia / Ogólne / Członkostwo ) </li>
    <li> Instalujemy certyfikat SSL </li>
    <li> Ustawiamy inny prefix dla tabel w bazie danych niż ten standardowy ( 'wp_' ) </li>
    <li> Generujemy własne klucze zabezpieczające dane przechowywane w ciasteczkach ( Własne klucze można wygenerować tutaj: https://api.wordpress.org/secret-key/1.1/salt/ ) </li>
    <li> Przenosimy dane bazy. Skoro jesteśmy w pliku wp-config.php to szukamy fragmentu:
      <pre>
define('DB_NAME', 'moja_baza');
define('DB_USER', 'moj_user');
define('DB_PASSWORD', 'moje_haslo');
define('DB_HOST', 'moj_host');
define('DB_CHARSET', 'utf8');
define('DB_COLLATE', '');
</pre>

i kopiujemy je do innego pliku – przykładowo wp-config-data.php a następnie w pliku wp-config.php dodajemy

require_once "wp-config-data.php";
  </ul>
</li>

<li> Instalujemy WP </li>
