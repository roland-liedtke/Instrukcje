# Optymalizacja

1. Google PageSpeed Insights
2. Pingdom Tools
3. GTMetrix
4. Wtyczka pamięci podręcznej
Wtyczka pamięci podręcznej generuje statyczne strony HTML Twojej witryny i zapisuje je na serwerze. Za każdym razem, gdy użytkownik próbuje uzyskać dostęp do treści strony, omawiana wtyczka wyświetla lżejszą stronę HTML zamiast ciężkich skryptów PHP WordPressa.

Wtyczka pamięci podręcznej niejako „przechowuje” daną zawartość, aby wstępnie załadować ją szybciej, gdy ktoś akurat będzie próbował wejść na stronę. Gdy zasoby statyczne, takie jak obrazy i pliki JavaScript, są przeładowywane za każdym razem, gdy tylko są wymagane, bardzo spowalnia to działanie witryny.

5. Optymalizacja zdjęć i lazy loading
Optymalizacja zdjęć w WordPress to jeden z prostszych, a zarazem najskuteczniejszych sposobów na poprawę szybkości ładowania witryny. W wielu przypadkach wagę plików graficznych można zmniejszyć nawet kilkukrotnie, zachowując przy tym wysoką jakość. Jeśli chcesz w ten sposób przyśpieszyć WordPressa, najlepiej skorzystaj ze specjalnych rozszerzeń, które automatyzują to zadanie (np. Imagify).

Z kolei lazy loading to technika, która sprawia, że obrazy i filmy na stronie internetowej są ładowane tylko wtedy, gdy stają się widoczne w obrębie pola widocznego właśnie dla użytkownika. Znacznie poprawia to szybkość strony internetowej, ponieważ zmniejsza ilość danych, które muszą być początkowo przygotowane, co pozwala osiągnąć krótszy czas ładowania i zapewnia lepsze doświadczenie użytkownika. Leniwe ładowanie na stronie WordPress można wdrożyć za pomocą wtyczek lub dodając odpowiednie fragmenty kodu do pliku functions.php strony.

5 najlepszych praktyk optymalizacji wydajności WordPress
Jak przyspieszyć ładowanie strony WordPress za pomocą innych skutecznych, podstawowych metod? Przeanalizujmy kilka z nich.

1. Korzystaj z najnowszej wersji PHP
Korzystanie z najnowszej wersji PHP ma znaczący wpływ na szybkość i wydajność witryny WordPress. PHP to język programowania, który zasila tego CMS-a, a jego aktualizacje mogą przyczynić się do poprawy wydajności, bezpieczeństwa i funkcjonalności.

Warto jednak pamiętać, że aktualizacja do najnowszej wersji PHP może również uszkodzić stronę internetową, jeśli zawiera ona kod, który nie jest już kompatybilny z nowym wydaniem. Z tego powodu przed taką zmianą warto przeprowadzić testy zgodności.

2. Ogranicz liczbę wykorzystywanych pluginów
Zbyt duża liczba pluginów (zwłaszcza przestarzałych) może przeszkodzić w przyspieszaniu strony WordPress. Regularnie usuwaj zatem te, których nie używasz. Staraj się także korzystać z mniejszej liczby rozszerzeń, które gromadzą w sobie liczne funkcje, zamiast polegać na pomniejszych.

3. Regularnie czyść bibliotekę multimediów
Kolejnym prostym i skutecznym sposobem na przyspieszenie WordPressa jest regularne czyszczenie niewykorzystywanych mediów. Z biegiem czasu może nagromadzić się ich całkiem sporo, przez co zaczną negatywnie wpływać na funkcjonowanie witryny. To zadanie ułatwiają różne pluginy jak np. Media Cleaner.

4. Nie hostuj treści video na serwerze
Skoro mowa o multimediach, to treści video zdecydowanie zajmują najwięcej miejsca. Nie musisz jednak ograniczać tego, w jakim zakresie z nich korzystasz. Aby zoptymalizować prędkość WordPressa, po prostu opublikuj je na innych serwisach jak YouTube lub Vimeo, a na samej stronie przedstawiaj je w wersji zagnieżdżonej.

5. Ogranicz maksymalną liczbę komentarzy wyświetlanych w danym momencie
Jak przyspieszyć bloga WordPress? Choć zapewne chciałbyś, aby pod artykułami znajdowało się mnóstwo komentarzy czytelników, to jednak za duże ich nagromadzenie może czasami przyczynić się do gorszej szybkości ładowania.

Dlatego warto ograniczyć to, ile komentarzy może wyświetlać się w danym momencie na stronie. W tym celu wykonaj następujące kroki:

1. Ogranicz lub wyłącz przechowywanie zmienionych wersji artykułów
Za każdym razem, gdy zapisujesz jakiś wpis, WordPress automatycznie tworzy kopie jego wersji i przechowuje je w swojej bazie danych. Dzięki temu możesz powrócić do dowolnego wariantu swojego postu, jeśli kiedykolwiek będziesz tego potrzebować.

Chociaż jest to pomocna funkcja, to jednak może przeszkadzać w zwiększaniu prędkości strony, jeśli kopie zapasowe nagromadzą się w zbyt dużej liczbie. Domyślnie WordPress zapisuje nieograniczoną liczbę poprawek postów, ale za pomocą małej modyfikacji można wyłączyć tę funkcję.

Aby to zrobić, otwórz plik WordPress wp-config.php i dodaj do niego następującą linię konfiguracyjną na samym dole:

define('WP_POST_REVISIONS', false);
Jeśli chcesz jedynie ograniczyć liczbę zapisywanych wersji, zamiast „false” wpisz konkretną liczbę.

2. Korzystaj z Content Delivery Network
Bez względu na lokalizację użytkownika, treści zawarte na Twojej stronie powinny być dostarczane błyskawicznie. Czasami jednak nie jest to możliwe, jeśli np. witryna nie jest obsługiwana przez infrastrukturę, która zawiera centra danych także w innych częściach świata. Odległość może wtedy oznaczać opóźnienia w dostarczaniu contentu.

Właśnie w takiej sytuacji, w celu optymalizacji WordPressa, warto skorzystać z sieci dostarczania treści. Pozwala ona przyspieszyć wczytywanie się strony WordPress, gdyż sprawia, że podczas przedstawiania treści Twoja witryna będzie korzystać z najbardziej zoptymalizowanego serwera, znajdującego się najbliższej fizycznej lokalizacji użytkownika.

3. Wprowadź minifikację kodu
Z czasem CSS, HTML i inne pliki kodu źródłowego mogą się nawarstwiać i powodować, że Twoja strona będzie działać coraz wolniej. Aby temu zaradzić, powinieneś rozważyć zminifikowanie kodu.

Celem minifikacji jest zmniejszenie rozmiaru plików HTML, JavaScript i CSS, a także usunięcie zbędnych znaków, takich jak spacje, przerwy między wierszami i komentarze. Dzięki temu pliki są lepiej zoptymalizowane, a strona ładuje się szybciej.

4. Unikaj przekierowań
Od czasu do czasu strony są usuwane i przenoszone, a kiedy indziej musisz zmienić strukturę swojej witryny. W takich sytuacjach najlepszym sposobem na uniknięcie błędów 404 jest wdrożenie stałych przekierowań. Mimo to staraj się ograniczyć ich liczbę. Każde przekierowanie zwiększa czas ładowania strony. Jest tak zwłaszcza wtedy, gdy powstają łańcuchy przekierowań i odwiedzający są ciągle odsyłani do innych adresów.

Przekierowania są często nieuniknione, ale wczesna optymalizacja WordPressa pod kątem architektury pozwoli ograniczyć je do minimum.

5. Ogranicz liczbę zewnętrznych skryptów
Zewnętrzne skrypty są wykorzystywane przez stronę, jednak nie są przechowywane na Twoim serwerze (przykładowo Google Analytics). Jeśli zatem zastanawiasz się nad skorzystaniem z wtyczki, która funkcjonuje właśnie w takiej formie, tym bardziej zastanów się nad tym, jak może wpłynąć na wydajność witryny.

Podsumowanie
Skuteczne przyspieszenie WordPressa jest możliwe, choć wymaga czasu i umiejętności. Mamy nadzieję, że dzięki temu artykułowi już wiesz, na czym polega ten proces.
