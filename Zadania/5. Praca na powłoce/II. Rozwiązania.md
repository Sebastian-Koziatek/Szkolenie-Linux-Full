# Rozwiązania - Praca na powłoce

## 1. Sprawdź, w jakim katalogu aktualnie się znajdujesz.

```
Polecenie:
pwd

Wyjaśnienie:
- pwd = Print Working Directory
- Pokazuje pełną ścieżkę bieżącego katalogu
- Używa absolutnej ścieżki (zaczynającej się od /)

Przykładowe wyjście:
/home/username
/Users/username (macOS)
/root (gdy jesteś rootem)
```

## 2. Wyświetl zawartość bieżącego katalogu.

```
Podstawowe polecenie:
ls

Dodatkowe opcje:
ls -l      # Długi format z szczegółami
ls -la     # Włącznie z plikami ukrytymi
ls -lh     # Z rozmiarem w czytelnym formacie
ls -lt     # Sortowane według czasu modyfikacji
ls -lS     # Sortowane według rozmiaru

Informacje w ls -l:
drwxr-xr-x  2 user group  4096 Oct 23 10:30 katalog
-rw-r--r--  1 user group  1024 Oct 23 10:25 plik.txt

Pierwszy znak: d=katalog, -=plik, l=link
Następne 9 znaków: uprawnienia (właściciel, grupa, inni)
Liczba: liczba linków
user: właściciel
group: grupa
4096: rozmiar w bajtach
Data i czas: ostatnia modyfikacja
```

## 3. Utwórz nowy katalog o nazwie `szkolenie` w bieżącej lokalizacji.

```
Polecenie:
mkdir szkolenie

Weryfikacja:
ls -ld szkolenie

Dodatkowe opcje mkdir:
mkdir -p ścieżka/do/katalogu    # Tworzy całą ścieżkę rekurencyjnie
mkdir -m 755 szkolenie          # Ustawia konkretne uprawnienia
mkdir katalog1 katalog2         # Tworzy wiele katalogów jednocześnie

Przykład tworzenia zagnieżdżonych katalogów:
mkdir -p projekt/src/main/java
```

## 4. Przejdź do katalogu `szkolenie`.

```
Polecenie:
cd szkolenie

Weryfikacja:
pwd

Inne sposoby nawigacji:
cd /ścieżka/absolutna          # Ścieżka absolutna
cd ../katalog                  # Ścieżka względna
cd ~                          # Katalog domowy użytkownika
cd -                          # Poprzedni katalog
cd                            # Katalog domowy (bez argumentu)
cd ..                         # Katalog wyżej

Przydatne zmienne środowiskowe:
$HOME - katalog domowy
$OLDPWD - poprzedni katalog
$PWD - bieżący katalog
```

## 5. Utwórz pięć plików: `plik1`, `plik2`, `plik3`, `plik4`, `plik5` – za pomocą jednego polecenia.

```
Różne sposoby:

Touch z wieloma argumentami:
touch plik1 plik2 plik3 plik4 plik5

Touch z brace expansion:
touch plik{1,2,3,4,5}
touch plik{1..5}

Seq z xargs:
seq 1 5 | xargs -I {} touch plik{}

For loop w jednej linii:
for i in {1..5}; do touch plik$i; done

Weryfikacja:
ls -l plik*
```

## 6. Utwórz ukryty plik o nazwie `.ukryty.txt`.

```
Polecenie:
touch .ukryty.txt

Wyjaśnienie:
- Pliki ukryte w Linux zaczynają się od kropki (.)
- Nie są wyświetlane przez standardowe ls
- Są widoczne z opcją ls -a

Inne sposoby tworzenia plików:
echo "" > .ukryty.txt
cat > .ukryty.txt
# (Ctrl+D aby zakończyć)

Weryfikacja istnienia:
ls -la .ukryty.txt
file .ukryty.txt
```

## 7. Wyświetl pełną zawartość katalogu, łącznie z plikami ukrytymi.

```
Polecenie:
ls -la

Alternatywy:
ls -al      # Identyczne
ls -a -l    # To samo, oddzielne opcje
ll -a       # Jeśli ll jest aliasem dla ls -l

Wyjaśnienie opcji:
-l: długi format (long)
-a: wszystkie pliki (all), włącznie z ukrytymi

Przykładowe wyjście:
total 24
drwxr-xr-x  2 user group 4096 Oct 23 10:30 .
drwxr-xr-x  3 user group 4096 Oct 23 10:25 ..
-rw-r--r--  1 user group    0 Oct 23 10:30 .ukryty.txt
-rw-r--r--  1 user group    0 Oct 23 10:30 plik1
-rw-r--r--  1 user group    0 Oct 23 10:30 plik2
...

Specjalne katalogi:
. - bieżący katalog
.. - katalog nadrzędny
```

## 8. Zmień nazwę pliku `.ukryty.txt` na `plik6`.

```
Polecenie:
mv .ukryty.txt plik6

Wyjaśnienie:
- mv = move (przenieś)
- Służy do przenoszenia i zmiany nazwy
- Pierwszy argument: źródło
- Drugi argument: cel

Weryfikacja:
ls -la | grep plik6
ls -la .ukryty.txt  # Powinno pokazać "No such file"

Inne użycia mv:
mv plik katalog/           # Przeniesienie do katalogu
mv plik1 plik2 katalog/    # Przeniesienie wielu plików
mv katalog1 katalog2       # Zmiana nazwy katalogu
mv *.txt backup/           # Przeniesienie wszystkich plików .txt
```

## 9. Zapisz tekst `Szkolenie Linux` do pliku `plik3`.

```
Różne sposoby:

Echo z przekierowaniem:
echo "Szkolenie Linux" > plik3

Printf:
printf "Szkolenie Linux\n" > plik3

Cat z heredoc:
cat > plik3 << EOF
Szkolenie Linux
EOF

Tee:
echo "Szkolenie Linux" | tee plik3

Weryfikacja:
cat plik3
head plik3
less plik3

Różnica między > i >>:
> - nadpisuje plik (truncate)
>> - dopisuje na końcu pliku (append)
```

## 10. Wyświetl zawartość pliku `plik3`.

```
Podstawowe polecenia:

Cat (najczęściej używane):
cat plik3

Less (dla większych plików):
less plik3
# q - wyjście, spacja - następna strona, b - poprzednia strona

More (starsze, mniej funkcjonalne):
more plik3

Head (pierwsze linie):
head plik3
head -n 5 plik3    # Pierwsze 5 linii

Tail (ostatnie linie):
tail plik3
tail -n 5 plik3    # Ostatnie 5 linii

Grep (wyszukiwanie):
grep "Linux" plik3
```

## 11. Z aktualnej lokalizacji utwórz folder `/tmp/test`.

```
Polecenie:
mkdir -p /tmp/test

Wyjaśnienie:
- Używamy ścieżki absolutnej (/tmp/test)
- Opcja -p tworzy katalogi rekurencyjnie
- Jeśli /tmp nie istnieje, zostanie utworzony
- Opcja -p nie zgłasza błędu jeśli katalog już istnieje

Weryfikacja:
ls -ld /tmp/test
ls -la /tmp/ | grep test

Bez opcji -p (gdyby /tmp nie istniał):
mkdir: cannot create directory '/tmp/test': No such file or directory
```

## 12. Czym jest katalog `/tmp`? Jakie ma właściwości?

```
Katalog /tmp (temporary):

Przeznaczenie:
- Przechowywanie plików tymczasowych
- Pliki mogą być usunięte przy restarcie systemu
- Dostępny dla wszystkich użytkowników

Właściwości:
- Uprawnienia: drwxrwxrwt (sticky bit)
- Sticky bit (t): tylko właściciel może usuwać swoje pliki
- World-writable: każdy może tworzyć pliki
- Często montowany jako tmpfs (w pamięci RAM)

Lokalizacja w różnych systemach:
/tmp - standardowy katalog tymczasowy
/var/tmp - dla plików o dłuższym czasie życia
/dev/shm - shared memory (tmpfs)

Zarządzanie:
- systemd-tmpfiles czyści stare pliki
- tmpwatch usuwa niewykorzystane pliki
- Polityki czyszczenia konfigurowalne

Sprawdzenie typu systemu plików:
df -T /tmp
mount | grep tmp

Zmienne środowiskowe:
$TMPDIR - katalog tymczasowy dla aplikacji
$TMP, $TEMP - alternatywne zmienne

Bezpieczeństwo:
- Uważaj na race conditions
- Używaj mktemp do tworzenia bezpiecznych nazw
- Sprawdzaj uprawnienia plików
```

## 13. Skopiuj całą zawartość bieżącego katalogu do `/tmp/test`.

```
Polecenie:
cp -r * /tmp/test/

Wyjaśnienie opcji:
-r: rekurencyjnie (dla katalogów)
*: wszystkie pliki i katalogi (wildcard)

Alternatywne metody:

Kopiowanie z ukrytymi plikami:
cp -r .* * /tmp/test/ 2>/dev/null

Rsync (bardziej zaawansowane):
rsync -av . /tmp/test/

Find z exec:
find . -type f -exec cp {} /tmp/test/ \;

Tar (kopiowanie przez archiwum):
tar -cf - . | (cd /tmp/test && tar -xf -)

Uwagi:
- cp * nie kopiuje plików ukrytych (zaczynających się od .)
- Opcja -a zachowuje atrybuty (timestamps, permissions)
- Opcja -v pokazuje kopiowane pliki (verbose)

Weryfikacja:
ls -la /tmp/test/
```

## 14. Wyświetl zawartość katalogu `/tmp/test`.

```
Polecenie:
ls -la /tmp/test

Alternatywy:
ls -la /tmp/test/
find /tmp/test -ls
tree /tmp/test (jeśli zainstalowane)

Porównanie z oryginalnym katalogiem:
ls -la szkolenie
ls -la /tmp/test

Sprawdzenie czy kopiowanie się udało:
diff -r . /tmp/test/

Liczenie plików:
ls -1 /tmp/test | wc -l
find /tmp/test -type f | wc -l
```

## 15. Przejdź jeden katalog wyżej.

```
Polecenie:
cd ..

Weryfikacja:
pwd

Wyjaśnienie:
.. - katalog nadrzędny (parent directory)
. - bieżący katalog (current directory)

Inne sposoby:
cd $OLDPWD  # Poprzedni katalog
cd -        # Poprzedni katalog (skrót)

Przejście o wiele poziomów wyżej:
cd ../..       # Dwa poziomy wyżej
cd ../../..    # Trzy poziomy wyżej

Sprawdzenie ścieżki:
pwd
echo $PWD
```

## 16. Wyświetl zawartość `/tmp`, pokazując tylko folder `test`.

```
Polecenia:

Grep z ls:
ls -la /tmp | grep test

Ls z wzorcem:
ls -ld /tmp/test

Find:
find /tmp -maxdepth 1 -name "test" -type d

Ls z wildcard:
ls -ld /tmp/test*

Tylko nazwa (bez szczegółów):
ls /tmp | grep "^test$"

Sprawdzenie typu:
file /tmp/test
ls -ld /tmp/test | grep "^d"
```

## 17. Przejdź do katalogu `/tmp/test` i usuń wszystkie znajdujące się w nim pliki.

```
Kroki:
1. cd /tmp/test
2. rm *

Alternatywne metody usuwania:

Wszystkie pliki (bez katalogów):
rm -f *

Wszystkie pliki włącznie z ukrytymi:
rm -f .* *
rm -f .[^.]* ..?* *  # Bezpieczniejsze

Tylko pliki (nie katalogi):
find . -type f -delete
find . -maxdepth 1 -type f -exec rm {} \;

Z potwierdzeniem:
rm -i *

Bez pytań:
rm -f *

Weryfikacja:
ls -la
# Powinno pokazać tylko . i ..

Uwagi bezpieczeństwa:
- Sprawdź pwd przed rm *
- Używaj rm -i dla ważnych danych
- Rozważ backup przed usuwaniem
- Uważaj na spacje w nazwach plików
```

## 18. Wróć katalog wyżej.

```
Polecenie:
cd ..

Alternatywy:
cd /tmp
cd $OLDPWD (jeśli wcześniej byłeś w /tmp)

Weryfikacja lokalizacji:
pwd
# Powinno pokazać: /tmp

Inne sposoby nawigacji:
cd -    # Toggle między dwoma ostatnimi katalogami
popd    # Jeśli używasz pushd/popd stack
```

## 19. Usuń pusty katalog `test`.

```
Polecenie:
rmdir test

Alternatywy:
rm -d test    # Nowsze wersje rm
rm -rf test   # Usuwa rekurencyjnie (nawet niepusty)

Wyjaśnienie:
- rmdir usuwa tylko puste katalogi
- Zgłosi błąd jeśli katalog nie jest pusty
- rm -rf usuwa rekurencyjnie wszystko

Weryfikacja:
ls -la | grep test
ls -ld test  # Powinno pokazać "No such file or directory"

Sprawdzenie czy katalog jest pusty:
ls -la test
find test -mindepth 1 -print -quit
```

## 20. Przejdź do katalogu domowego użytkownika.

```
Różne sposoby:

Najkrótszy:
cd

Używając tyldy:
cd ~

Używając zmiennej HOME:
cd $HOME

Pełna ścieżka:
cd /home/username     # Linux
cd /Users/username    # macOS

Dla innego użytkownika:
cd ~username

Weryfikacja:
pwd
echo $HOME

Sprawdzenie gdzie jesteśmy:
whoami
id
```

## 21. Wyświetl historię ostatnio używanych poleceń.

```
Podstawowe polecenie:
history

Opcje history:
history 10        # Ostatnie 10 poleceń
history | tail    # Ostatnie polecenia
history | head    # Pierwsze polecenia
history | grep ls # Wszystkie polecenia zawierające "ls"

Numeracja w historii:
!123     # Wykonaj polecenie numer 123
!!       # Ostatnie polecenie
!-2      # Przedostatnie polecenie
!ls      # Ostatnie polecenie zaczynające się od "ls"

Pliki historii:
~/.bash_history    # Bash
~/.zsh_history     # Zsh
~/.history         # Niektóre shelle

Zmienne środowiskowe:
$HISTSIZE - rozmiar historii w pamięci
$HISTFILE - plik historii
$HISTFILESIZE - rozmiar pliku historii

Czyszczenie historii:
history -c    # Wyczyść historię w pamięci
history -w    # Zapisz historię do pliku
> ~/.bash_history  # Wyczyść plik historii
```

## 22. Zapisz historię poleceń do pliku `historia.txt`.

```
Różne sposoby:

History z przekierowaniem:
history > historia.txt

History z ostatnimi N poleceniami:
history 50 > historia.txt

Z numeracją:
history | cat -n > historia.txt

Bez numerów (tylko polecenia):
history | cut -d' ' -f2- > historia.txt
history | sed 's/^[ ]*[0-9]*[ ]*//' > historia.txt

Dopisanie na koniec:
history >> historia.txt

Z timestampem:
HISTTIMEFORMAT="%F %T " history > historia.txt

Weryfikacja:
cat historia.txt
wc -l historia.txt
head -5 historia.txt
tail -5 historia.txt

Kopiowanie pliku historii:
cp ~/.bash_history historia.txt

Filtrowanie historii:
history | grep -v "history" > historia.txt  # Bez poleceń history
```