# Instalacja WordPress przez FTP ( File Transfer Protocol )

<ol>
  <li> Potrzebny będzie nam klient FTP (np. FileZilla) </li>
  <li> Ogarniamy dane do FTP (host, login, hasło, protokół i port (dwa ostatnie to najczęściej FTP / 21) </li>
  <li> Pobieramy pliki WordPress ( https://pl.wordpress.org/download/ ) </li>
  <li> Rozpakowujemy zip lokalnie i wrzucamy pliki na serwer </li>
  <li> Tworzymy bazę danych w panelu hostingu ( nazwa bazy, nazwa użytkownika, hasło ). Warto również sprawdzić jaki jest host – czy będzie to localhost czy jest w panelu hostingu podane coś innego. <br>
    <strong>UWAGA: </strong> Pamiętaj by dać jakieś mało oczywiste hasło i nazwę użytkownika.</li>
<li> Uzupełniamy dane bazy w pliku wp-config. W plikach, które wgraliśmy szukamy wp-config-sample.php i zmieniamy mu nazwę na wp-config.php. Następnie otwieramy plik w edytorze tekstowym i w miejscu na dane bazy wpisujemy to co udało nam się wyczarować w panelu hostingowym. 
  <ul>
    <li> Po pierwsze: Zmieniamy prefix bazy danych z wp_ na coś innego </li>
    <li> Po drugie: generujemy własne klucze zabezpieczające dane przechowywane w ciasteczkach </li>
    <li> Po trzecie: przenosimy dane bazy do osobnego pliku </li>
    <li> Po czwarte: ukrywamy błędy na stronie </li>
    <li> Po piąte: wyłączamy możliwość edycji plików motywu i wtyczek bezpośrednio przez panel WordPress </li>
  </ul>
</li>

<li> Instalujemy WP </li>
