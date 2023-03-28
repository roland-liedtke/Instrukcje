// Pobieranie obrazu ISO systemu Linux Debian
1. Na stronie https://www.debian.org/index.pl.html znajduje się przycisk 
Pobieranie, po kliknięciu tego przycisku przeniesie nas do zakładki 
https://www.debian.org/download skąd pobieramy plik 
debian-11.6.0-amd64-netinst.iso (".iso" jest to obraz dysku). 

// Konfiguracja maszyny wirtualnej w VirtualBox
2. Następnym krokiem będzie uruchomienie aplikacji Oracle VM VirtualBox 
dzięki której stworzymy maszynę wirtualną, na której zainstalujemy 
wcześniej pobrany system Linux Debian.

3. Po otwarciu aplikacji klikamy przycisk o nazwie Nowa (niebieska 
gwiazdka). 
Otworzyło nam się nowe okno, gdzie podajemy:
- Nazwę ( będzie służyła do 
identyfikacji VM w VirtualBoxie), 
- Folder gdzie będzie się znajdowała VM, 
- dodatkowo możesz wybrać obraz ISO, który zostanie użyty do instalacji 
systemu (po wyborze tej opcji pozostałe pola zostaną wyłączone),
- Typ systemu np. Windows, Linux, Mac OS X,
- Wersja wyżej wybranego typu systemu,
- checkbox (domyślnie wyłączony i nieaktywny), który włącza manualną 
instalację. 
Po wyborze obrazu ISO checkbox się uaktywnia i pozwala na wybór instalacji 
manualnej lub automatycznej. Po wypełnieniu pól klikamy przycisk Next, 
który przenosi nas do kolejnego kroku.

Moja konfiguracja:
Nazwa: Linux-Debian
Folder: C:\Users\roland\VirtualBox VMs\Linux-Debian
Obraz ISO: C:\Users\roland\Downloads\
Checkbox: check & active

4. Aktualnie mamy możliwość zarezerwowania odpowiedniej ilości pamięci 
RAM, liczby procesorów CPU oraz dysku twardego. Do wyboru mamy:
- utworzenie nowego wirtualnego dysku twardego,
- użycie istniejącego wirtualnego dysku,
- nie dodawać wirtualego dysku. 

Moja konfiguracja:
RAM: 2048 MB
CPU: 1
new Virtual HDD: 20 GB

5. Po odpowiedniej konfiguracji widzimy okno o nazwie Podsumowanie, które 
przypomina nam wcześniejszą konfigurację. Jeżeli wszystko się zgadza, 
klikamy przycisk Zakończ.
Na tym kończymy konfigurację VM, klikamy przycik Uruchom i bierzemy 
gaśnicę do ręki (safety first!).

6. Po uruchomieniu systemu powinien wyświetlić nam się BIOS mode, w którym 
możemy wybrać szczegóły instalacji. Wybieramy metodę instalacji i 
następnie wybieramy: 
- język, który będzie domyślnym językiem systemu, 
- określamy swoją lokalizację w celu ustalenia strefy czasowej,
- konfigurację klawiatury,

Moja konfiguracja:
Język: Polski
Kraj: Polska
Klawiatura: polski

7. Kolejna konfiguracja dotyczy sieci, należy wprowadzić nazwę hosta dla 
tego systemu oraz domenę.

Moja konfiguracja:
Nazwa hosta: debian
Domena: ""

8. Teraz czas na ustalenie hasła dla root'a - administratora systemu. 
UWAGA: Użytkownik root nie powinien mieć pustego hasła. Jeśli zostawisz je 
puste konto roota zostanie zablokowane, a konto użytkownika założone 
podczas instalacji otrzyma możliwość zalogowania się na roota za pomocą 
polecenia "sudo".

Moja konfiguracja:
Hasło: root

9. Tworzymy teraz konto użytkownika do celów nie związanych z czynnościami 
administracyjnymi. 

Moja konfiguracja:
Nazwa użytkownika: Roland Liedtke
Konto: roland
Hasło: 1234

// UZUPEŁNIJ PO ZDOBYCIU WIEDZY
10. Kolejny krok to partycjonowanie dysku. Klikamy Ręcznie, aby wybrać 
wcześniej utworzony dysk wirtualny podczas konfiguracji VM.

Moja konfiguracja:
SCSI (0,0,0) (sda) - 21.5 GB ATA VBOX HARDDISK
ext4 

11. Po instalacji pojawi się komunikat o Konfiguracji menedżera pakietów 
(apt). Masz teraz możliwość przeskanowania dodatkowych nośników.

Moja konfiguracja:
<Nie>
Serwer lustrzany: Polska
deb.debian.org
Dane serwera pośredniczącego: ""

12. Kolejny kominikat "Konfiguracja pakietu popularity-contest". Możesz 
sprawić, że Tój system będzie anonimowo przesyłał deweloperom informację o 
najczęściej używanych przez Ciebie pakietach.

Moja konfiguracja: <Nie>

13. Wybór oprogramowania - w tym momencie tylko podstawowy system jest 
zainstalowany. Do wybrou oprogramowanie:
[*] Podstawowe składniki środowiska graficznego Debiana
[*] Środowisko GNOME
[ ] Środowisko Xfce
[ ] Środowisko GNOME Flashback
[ ] KDE Plasma
[ ] Cinnamon
[ ] MATE
[ ] Środowisko LXDE
[ ] LXQt
[ ] Serwer WWW
[*] Serwer SSH
[*] Podstawowe narzedzia systemowe

// UZUPEŁNIJ PO ZDOBYCIU WIEDZY
14. Instalacja programu rozruchowego GRUB

Klikamy <Tak>

Następnie wybieramy urządzenie do instalacji programu rozruchowego.

/dev/sda (ata-VBOX_HARDDISK)

Następnie klikamy Zakończ instalację <Dalej>

15. Uruchamia nam się okno rozruchowe GRUB do wyboru, po krótkim czasie 
bezczynności system sam wybierze domyślną pozycję.

16. Powinno pojawić się okno z nazwą użytkownika i logiem Debiana - to 
znak, że instalacja systemu przebiegła pomyślnie.
