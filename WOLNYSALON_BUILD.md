# Klient pomocy zdalnej Wolny Salon

Źródło: RustDesk OSS 1.5.0 (AGPL-3.0). Ten wariant jest przeznaczony wyłącznie
dla Windows i macOS. Ustawienia serwera są domyślne dla nowej instalacji, a nie
sekretem ani blokadą zmiany serwera przez użytkownika.

## Konfiguracja

`patches/wolnysalon-hbb-common.patch` ustawia serwer `57.128.178.147`, jego
klucz publiczny i oddzielną nazwę konfiguracji `WolnySalonPomoc`. Dla macOS
ustawia też organizację `pl.wolnysalon`. Projekt macOS ma osobny identyfikator
aplikacji. Klucz prywatny serwera nie znajduje się w tym repozytorium.

## Kompilacja w CI

W GitHub Actions uruchom `Wolny Salon remote support clients` i wybierz
`windows` lub `macos`. Obie platformy należy uruchomić osobno. Akcja używa
oryginalnego łańcucha kompilacji RustDesk, ale po pobraniu submodułu nakłada
łatkę z ustawieniami Wolnego Salonu. Wyniki są publikowane jako wersja wstępna
`wolnysalon-1.5.0-<numer przebiegu>`. Nie kopiuj ich do katalogu pobierania
salonu, zanim przejdą testy poniżej.

## Test przed publikacją

1. Sprawdź, czy przebieg CI zakończył się bez błędów i pobierz paczkę z wydania.
2. Na czystym profilu Windows i macOS sprawdź, czy aplikacja pokazuje serwer
   `57.128.178.147` bez ręcznego wpisywania adresu ani klucza.
3. Zweryfikuj odcisk klucza publicznego serwera i połączenie z serwerem pomocy.
4. Zestaw próbne połączenie za zgodą użytkownika i sprawdź zakończenie sesji.
5. Sprawdź instalację obok zwykłego RustDesk i zachowanie po ponownym uruchomieniu.
6. Zapisz sumy SHA-256 paczek i udostępnij klientom dopiero przetestowane pliki.

Windows bez certyfikatu podpisu kodu może wyświetlić SmartScreen. macOS bez
Apple Developer ID nie może mieć podpisu Developer ID i notaryzacji; Gatekeeper
może wymagać ręcznego zatwierdzenia. Nie obchodź tych ostrzeżeń automatycznie.

Przy dystrybucji binariów udostępnij odpowiadający im kod źródłowy i informacje
o licencji AGPL-3.0.
