# Rozwiązania - Edytory tekstu

## 1. Utwórz nowy plik tekstowy o nazwie `temp.txt` za pomocą dowolnego edytora.

```
Różne sposoby utworzenia pliku temp.txt:

Nano:
nano temp.txt

Vi/Vim:
vi temp.txt
vim temp.txt

Gedit (w środowisku graficznym):
gedit temp.txt

Touch + edytor:
touch temp.txt
nano temp.txt

Echo:
echo "" > temp.txt
```

## 2. Wpisz do pliku frazę: `Szkolenie Linux`

```
W nano:
1. Otwórz: nano temp.txt
2. Wpisz: Szkolenie Linux
3. Tekst pojawia się bezpośrednio

W vi:
1. Otwórz: vi temp.txt
2. Naciśnij 'i' (tryb INSERT)
3. Wpisz: Szkolenie Linux
4. Naciśnij ESC (powrót do trybu COMMAND)
```

## 3. Zapisz plik i wyjdź z edytora.

```
W nano:
Ctrl+O (zapisz)
Enter (potwierdź nazwę pliku)
Ctrl+X (wyjdź)

W vi:
ESC (tryb COMMAND)
:wq (write and quit)
Enter

Alternatywne metody w vi:
:w (tylko zapisz)
:q (tylko wyjdź)
ZZ (zapisz i wyjdź - shortcut)
```

## 4. Otwórz plik `temp.txt` w edytorze `vi`.

```
Polecenie:
vi temp.txt

Po otwarciu:
- Plik otwiera się w trybie COMMAND
- Zawartość pliku jest widoczna
- Kursor znajduje się na początku pierwszego znaku
- Status line pokazuje informacje o pliku
```

## 5. Dopisz do istniejącej frazy słowa `jest proste` korzystając ze skrótu `A`.

```
Kroki w vi:
1. Upewnij się, że jesteś w trybie COMMAND (naciśnij ESC)
2. Naciśnij 'A' (duże A)
   - Kursor przeskoczy na koniec linii
   - Automatyczne przejście do trybu INSERT
3. Wpisz: " jest proste"
4. Naciśnij ESC (powrót do trybu COMMAND)

Rezultat: "Szkolenie Linux jest proste"

Inne przydatne skróty vi:
- a: append (wstaw po kursorze)
- A: append at end of line (wstaw na końcu linii)
- i: insert (wstaw przed kursorem)
- I: insert at beginning of line (wstaw na początku linii)
- o: open new line below (nowa linia poniżej)
- O: open new line above (nowa linia powyżej)
```

## 6. Wyjdź z edytora `vi` bez zapisywania zmian.

```
Polecenie w trybie COMMAND:
:q!

Wyjaśnienie:
: - przejście do trybu poleceń
q - quit (wyjdź)
! - force (wymuś, ignoruj niezapisane zmiany)

Inne opcje wyjścia z vi:
:q - wyjdź (tylko jeśli brak zmian)
:wq - zapisz i wyjdź
:x - zapisz i wyjdź (jeśli były zmiany)
ZQ - wyjdź bez zapisywania (shortcut)
ZZ - zapisz i wyjdź (shortcut)
```

## 7. Pobierz "Pana Tadeusza" w formacie `.txt` przy użyciu `wget`.

```
Polecenie:
wget https://wolnelektury.pl/media/book/txt/pan-tadeusz.txt

Proces:
1. wget nawiąże połączenie z serwerem
2. Pobierze plik pan-tadeusz.txt
3. Zapisze w bieżącym katalogu

Weryfikacja pobrania:
ls -la pan-tadeusz.txt
file pan-tadeusz.txt
wc -l pan-tadeusz.txt

Alternatywne źródła:
wget http://www.gutenberg.org/files/28564/28564-0.txt -O pan-tadeusz.txt
curl -o pan-tadeusz.txt https://wolnelektury.pl/media/book/txt/pan-tadeusz.txt

Opcje wget:
-O filename - zapisz pod konkretną nazwą
-c - kontynuuj przerwane pobieranie
-t 3 - maksymalnie 3 próby
--timeout=30 - timeout 30 sekund
```

## 8. Otwórz pobraną książkę (`pan-tadeusz.txt`) za pomocą edytora `vi`.

```
Polecenie:
vi pan-tadeusz.txt

Uwagi przy otwieraniu dużego pliku:
- Ładowanie może chwilę potrwać
- Vi/vim dobrze radzi sobie z dużymi plikami
- Plik otwiera się w trybie COMMAND
- Kursor na początku pierwszej linii

Podstawowe nawigacje w vi dla dużych plików:
G - przejdź na koniec pliku
gg - przejdź na początek pliku
:liczba - przejdź do konkretnej linii
Ctrl+F - strona w dół
Ctrl+B - strona w górę
Ctrl+D - pół strony w dół
Ctrl+U - pół strony w górę
```

## 9. Wyszukaj w tekście imię "Tadeusz" i przejdź przez kolejne wystąpienia.

```
Wyszukiwanie w vi:
1. Upewnij się, że jesteś w trybie COMMAND (ESC)
2. Wpisz: /Tadeusz
3. Naciśnij Enter
4. Vi znajdzie pierwsze wystąpienie i podświetli

Przechodzenie przez wystąpienia:
n - next (następne wystąpienie)
N - previous (poprzednie wystąpienie)

Dodatkowe opcje wyszukiwania:
/Tadeusz\c - wyszukiwanie bez uwzględnienia wielkości liter
?Tadeusz - wyszukiwanie wstecz
* - wyszukaj słowo pod kursorem (w przód)
# - wyszukaj słowo pod kursorem (w tył)

Zastępowanie:
:%s/Tadeusz/TADEUSZ/g - zamień wszystkie wystąpienia
:%s/Tadeusz/TADEUSZ/gc - zamień z potwierdzeniem

Highlight search:
:set hlsearch - podświetlanie wyników
:nohlsearch - wyłączenie podświetlania (lub :noh)
```

## 10. Uruchom plik `pan-tadeusz.txt` w edytorze `nano`.

```
Polecenie:
nano pan-tadeusz.txt

Charakterystyka nano:
- Edytor przyjazny dla początkujących
- Skróty klawiszowe wyświetlane na dole ekranu
- Bezpośrednia edycja (bez trybów jak w vi)
- Dobra obsługa dużych plików

Podstawowe skróty w nano:
Ctrl+G - pomoc (help)
Ctrl+X - wyjście (exit)
Ctrl+O - zapisz (write Out)
Ctrl+R - wczytaj plik (Read file)
Ctrl+W - wyszukaj (Where is)
Ctrl+K - wytnij linię (cut)
Ctrl+U - wklej (paste/Uncut)
Ctrl+C - pokaż pozycję kursora
```

## 11. Wyszukaj frazę `Tadeusz` i przejdź przez kolejne wystąpienia.

```
Wyszukiwanie w nano:
1. Naciśnij Ctrl+W
2. Wpisz: Tadeusz
3. Naciśnij Enter
4. Nano znajdzie pierwsze wystąpienie

Przechodzenie przez kolejne wystąpienia:
1. Naciśnij ponownie Ctrl+W
2. Naciśnij Enter (bez wpisywania - użyje ostatniego wyszukiwania)
3. Powtarzaj krok 2 dla kolejnych wystąpień

Alternatywna metoda:
Ctrl+W, wpisz "Tadeusz", Alt+W - kontynuuj wyszukiwanie

Dodatkowe opcje wyszukiwania w nano:
Alt+W - powtórz ostatnie wyszukiwanie
Ctrl+\ - znajdź i zamień (Where Is, then Replace)
Alt+R - wyszukiwanie z wyrażeniami regularnymi

Opcje wyszukiwania (po Ctrl+W):
Alt+C - case sensitive (wielkość liter)
Alt+B - backward search (wyszukiwanie wstecz)
Alt+R - regex search (wyrażenia regularne)
```

## 12. Wyjdź z edytora `nano` bez zapisywania zmian.

```
Kroki:
1. Naciśnij Ctrl+X (exit)
2. Jeśli były zmiany, nano zapyta: "Save modified buffer?"
3. Naciśnij 'N' (No)
4. Nano zamknie się bez zapisywania

Komunikaty nano:
"Save modified buffer? (Answering "No" will DISCARD changes.)"
- Y: Yes (zapisz)
- N: No (nie zapisuj)
- Ctrl+C: Cancel (anuluj wyjście)

Skróty wyjścia:
Ctrl+X - standardowe wyjście
Ctrl+C (dwukrotnie) - force exit w niektórych sytuacjach
```

## 13. Otwórz plik `temp.txt` za pomocą edytora `nano`.

```
Polecenie:
nano temp.txt

Po otwarciu:
- Plik wyświetla się w edytorze
- Kursor na początku pliku
- Skróty klawiszowe widoczne na dole ekranu
- Bezpośrednia możliwość edycji (brak trybów)

Status line pokazuje:
- Nazwę pliku
- Czy plik został zmodyfikowany
- Pozycję kursora (linia, kolumna)
```

## 14. Usuń cały wiersz za pomocą odpowiedniego skrótu.

```
Skrót w nano:
Ctrl+K - usuwa całą linię (cut line)

Proces:
1. Ustaw kursor gdziekolwiek w linii do usunięcia
2. Naciśnij Ctrl+K
3. Cała linia zostanie usunięta

Dodatkowe skróty usuwania w nano:
Alt+Del - usuń słowo po lewej stronie kursora
Ctrl+Del - usuń słowo po prawej stronie kursora
Alt+T - usuń od kursora do końca linii
Ctrl+U - wklej ostatnio wycięty tekst (uncut)

Wielokrotne usuwanie:
- Ctrl+K wykonane kilka razy usuwa kolejne linie
- Usunięte linie trafiają do bufora
- Można je przywrócić za pomocą Ctrl+U
```

## 15. Wpisz nową frazę: `Używam edytora nano`

```
Proces:
1. Po usunięciu poprzedniej linii kursor jest gotowy do wpisania
2. Wpisz bezpośrednio: Używam edytora nano
3. Tekst pojawia się natychmiast (brak trybów jak w vi)

Nano pozwala na:
- Bezpośrednie wpisywanie tekstu
- Użycie strzałek do nawigacji
- Standardowe zachowanie klawiatury
- Copy/paste systemowe (Ctrl+Shift+C/V w terminalu)
```

## 16. Zapisz zmiany i wyjdź z edytora.

```
Kroki:
1. Ctrl+O (WriteOut - zapisz)
   - Nano pokaże: "File Name to Write: temp.txt"
2. Naciśnij Enter (potwierdź nazwę pliku)
   - Komunikat: "[ Wrote 1 line ]"
3. Ctrl+X (Exit - wyjdź)
   - Nano zamknie się

Alternatywna metoda (szybsza):
Ctrl+X, następnie Y (tak, zapisz), Enter (potwierdź nazwę)

Opcje zapisu:
Ctrl+O - zapisz pod bieżącą nazwą
Alt+F - nowa nazwa pliku podczas zapisu
Ctrl+T - przeglądaj pliki (file browser)

Weryfikacja:
cat temp.txt
# Powinno pokazać: "Używam edytora nano"
```

## Dodatkowe zasoby i ćwiczenia

```
Przydatne strony do nauki vi/vim:
- https://vim.is/#exercise - interaktywne ćwiczenia
- https://www.openvim.com/ - tutorial online
- vimtutor - wbudowany tutorial (polecenie w terminalu)

Przydatne strony do nauki nano:
- man nano - pełna dokumentacja
- nano --help - szybki help
- https://www.nano-editor.org/dist/latest/cheatsheet.html

Porównanie edytorów:

Vi/Vim:
+ Bardzo potężny i konfigurowalny
+ Dostępny na każdym systemie Unix/Linux
+ Efektywny dla zaawansowanych użytkowników
- Stroma krzywa uczenia
- Tryby mogą być mylące dla początkujących

Nano:
+ Łatwy do nauki
+ Intuicyjny dla nowych użytkowników
+ Skróty wyświetlane na ekranie
- Mniej funkcji niż vim
- Może nie być domyślnie zainstalowany wszędzie

Emacs:
+ Bardzo rozszerzalny
+ Potężne funkcje programistyczne
- Bardzo złożony
- Duże zużycie zasobów
```