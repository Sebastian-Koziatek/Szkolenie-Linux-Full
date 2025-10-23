# Rozwiązania - Man i info

## 1. Użyj polecenia `man man` i zapoznaj się ze strukturą stron podręcznika (`man pages`).

```
Struktura stron podręcznika (man pages):

NAME - Nazwa polecenia i krótki opis
- Zawiera nazwę polecenia/programu
- Jednoliniowy opis funkcji

SYNOPSIS - Składnia polecenia
- Sposób użycia polecenia
- Opcjonalne i obowiązkowe parametry
- Konwencje: [] = opcjonalne, <> = wymagane, | = alternatywa

DESCRIPTION - Szczegółowy opis
- Dokładne wyjaśnienie działania
- Opis funkcjonalności
- Kontekst użycia

OPTIONS - Opcje i przełączniki
- Lista wszystkich dostępnych opcji
- Opis każdej opcji z przykładami
- Parametry krótkie (-h) i długie (--help)

EXAMPLES - Przykłady użycia
- Praktyczne przykłady komend
- Typowe scenariusze użycia
- Demonstracja różnych opcji

FILES - Pliki konfiguracyjne
- Ważne pliki systemowe związane z poleceniem
- Lokalizacje plików konfiguracyjnych

SEE ALSO - Zobacz również
- Powiązane polecenia i strony man
- Dodatkowe źródła informacji

BUGS - Znane błędy
- Opis znanych problemów
- Informacje o zgłaszaniu błędów

AUTHOR - Autor
- Informacje o twórcach
- Kontakt do opiekunów projektu

Sekcje man pages:
1 - Polecenia użytkownika
2 - Wywołania systemowe
3 - Funkcje biblioteczne
4 - Pliki specjalne (urządzenia)
5 - Formaty plików i konwencje
6 - Gry
7 - Różne (makra, konwencje)
8 - Polecenia administracyjne
9 - Procedury kernela
```

## 2. Przejrzyj stronę podręcznika dla polecenia `ls`.

```
Sekcja polecenia ls:
man ls pokazuje: LS(1) - sekcja 1 (polecenia użytkownika)

Opcje sortowania ls:
-t, --time - sortowanie według czasu modyfikacji
-S, --size - sortowanie według rozmiaru pliku
-X, --sort=extension - sortowanie według rozszerzenia
-v, --version-sort - sortowanie naturalne numerów wersji
-r, --reverse - odwrócenie kolejności sortowania
--sort=WORD - sortowanie według: none, size, time, version, extension

Przydatne przełączniki ls:

1. -l, --format=long
   - Długi format z szczegółami
   - Uprawnienia, właściciel, rozmiar, data

2. -a, --all
   - Pokazuje ukryte pliki (zaczynające się od .)
   - Włącznie z . i ..

3. -h, --human-readable
   - Rozmiary w czytelnym formacie (K, M, G)
   - Używane z -l

4. -R, --recursive
   - Rekurencyjne listowanie podkatalogów
   - Przechodzi przez całe drzewo katalogów

5. -F, --classify
   - Dodaje wskaźniki typu pliku
   - / dla katalogów, * dla executables

6. --color=auto
   - Kolorowanie według typu pliku
   - Ułatwia rozróżnianie typów

7. -i, --inode
   - Pokazuje numery i-node
   - Przydatne do diagnostyki systemu plików

8. -1 (cyfra jeden)
   - Jeden plik na linię
   - Przydatne w skryptach

9. -d, --directory
   - Lista katalogów bez ich zawartości
   - Pokazuje tylko sam katalog

10. -n, --numeric-uid-gid
    - Pokazuje UID i GID numerycznie
    - Zamiast nazw użytkowników/grup
```

## 3. Zainstaluj pakiet `info` i przejrzyj strukturę dokumentacji `info` dla polecenia `pwd`.

```
Instalacja pakietu info:
sudo yum install info          # RHEL/CentOS
sudo apt install info         # Debian/Ubuntu
sudo dnf install info         # Fedora

Struktura dokumentacji info vs man:

INFO:
- Hipertekstowy system dokumentacji
- Struktura węzłów (nodes) połączonych linkami
- Możliwość nawigacji między powiązanymi tematami
- Bardziej szczegółowa dokumentacja
- Integration z GNU projektem

MAN:
- Liniowa struktura dokumentu
- Czytanie od góry do dołu
- Krótsze, bardziej konkretne informacje
- Uniwersalny standard Unix/Linux

Różnice w nawigacji:

MAN:
- Przestronne: przewijanie w górę/dół
- /text: wyszukiwanie tekstu
- q: wyjście
- h: pomoc

INFO:
- n: next node (następny węzeł)
- p: previous node (poprzedni węzeł)
- u: up node (węzeł nadrzędny)
- TAB: następny link
- Enter: follow link (przejdź za link)
- l: last node (ostatni węzeł)
- d: directory node (katalog główny)
- q: quit (wyjście)
- ?: pomoc

Polecenie pwd w info:
info pwd
info coreutils 'pwd invocation'

Struktura dokumentacji pwd w info:
- Część większego manuala GNU coreutils
- Szczegółowe wyjaśnienie zachowania
- Przykłady użycia
- Linki do powiązanych poleceń
- Informacje o opcjach środowiska
```

## 4. Zainstaluj pakiet `mc` (Midnight Commander) i sprawdź dokumentację.

```
Instalacja Midnight Commander:
sudo yum install mc           # RHEL/CentOS
sudo apt install mc          # Debian/Ubuntu
sudo dnf install mc          # Fedora

Sprawdzenie dokumentacji mc:

1. Strona podręcznika man:
man mc
- TAK, mc posiada własną stronę man
- Szczegółowy opis funkcji
- Lista opcji wiersza poleceń
- Opis plików konfiguracyjnych

2. Dokumentacja info:
info mc
- Zwykle NIEDOSTĘPNA lub ograniczona
- mc nie jest częścią GNU Core Utilities
- Może być dostępna jako osobny pakiet

Przyczyny braku dokumentacji info:
- mc nie jest projektem GNU
- Preferuje własny system pomocy
- Dokumentacja man jest wystarczająca
- Focus na wbudowaną pomoc

3. Wbudowana pomoc w mc:

Uruchomienie pomocy:
- F1 podczas pracy z mc
- Ctrl+? jako alternatywa
- Menu Help > Contents

Funkcje wbudowanej pomocy:
- Interaktywna nawigacja
- Kontekstowa pomoc dla funkcji
- Lista skrótów klawiszowych
- Opis wszystkich opcji menu

Dodatkowe źródła pomocy mc:
- /usr/share/doc/mc/ - dokumentacja
- ~/.config/mc/ - pliki konfiguracyjne
- mc --help - podstawowa pomoc
- man mcedit - edytor tekstu mc

Wbudowane polecenia pomocy:
F1 - Pomoc główna
F2 - Menu użytkownika
F3 - Podgląd pliku
F4 - Edycja pliku
F9 - Menu główne
F10 - Wyjście

Skróty klawiszowe:
Alt+? - Quick help
Ctrl+O - Pokaż/ukryj panele
Alt+Tab - Przełącz panele
Ctrl+U - Zamień panele
```