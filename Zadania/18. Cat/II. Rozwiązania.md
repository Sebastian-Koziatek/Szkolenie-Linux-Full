# Rozwiązania - Cat

## 1. Wyświetlanie zawartości pliku na ekranie

```
Podstawowe polecenie cat:
cat plik.txt

Przykład:
cat /etc/passwd
cat ~/.bashrc
cat dokument.txt
```

## 2. Wyświetlanie zawartości wielu plików jednocześnie

```
Cat z wieloma plikami:
cat plik1.txt plik2.txt plik3.txt

Przykład:
cat /etc/hosts /etc/hostname
cat *.txt
cat dokument1.txt dokument2.txt

Wszystkie pliki z rozszerzeniem:
cat *.log
cat /var/log/*.log
```

## 3. Łączenie zawartości kilku plików i zapisywanie ich do nowego pliku

```
Przekierowanie do nowego pliku:
cat plik1.txt plik2.txt > nowy_plik.txt

Dopisywanie do istniejącego pliku:
cat plik3.txt >> nowy_plik.txt

Przykłady:
cat /etc/passwd /etc/group > users_info.txt
cat *.txt > wszystkie_teksty.txt
cat header.txt content.txt footer.txt > complete.txt
```

## 4. Wyświetlanie numerowanych linii w pliku

```
Cat z numerowaniem linii:
cat -n plik.txt

Numerowanie tylko niepustych linii:
cat -b plik.txt

Przykład:
cat -n /etc/passwd
cat -b ~/.bashrc

Porównanie:
-n: numeruje wszystkie linie
-b: numeruje tylko niepuste linie
```

## 5. Wyświetlanie zawartości pliku w odwróconej kolejności

```
Polecenie tac (cat odwrotnie):
tac plik.txt

Przykład:
tac /etc/passwd
tac ~/.bash_history

Alternative z sort:
sort -r plik.txt

Przykład zastosowania:
tac /var/log/messages | head -20  # Ostatnie 20 linii w odwróconej kolejności
```

## 6. Wyświetlanie tylko określonej liczby linii pliku

```
Pierwsze N linii:
head -n 10 plik.txt
head -10 plik.txt

Ostatnie N linii:
tail -n 10 plik.txt
tail -10 plik.txt

Z cat i head/tail:
cat plik.txt | head -5
cat plik.txt | tail -3

Przykłady:
head -5 /etc/passwd          # Pierwsze 5 linii
tail -10 /var/log/messages   # Ostatnie 10 linii
head -20 plik.txt | tail -5  # Linie 16-20
```

## 7. Wyświetlanie zawartości pliku z paginacją

```
Less (zalecane):
less plik.txt

More (starsze):
more plik.txt

Cat z paginacją przez pipe:
cat plik.txt | less
cat plik.txt | more

Skróty w less:
- Spacja: następna strona
- b: poprzednia strona  
- q: wyjście
- /słowo: wyszukiwanie
- n: następne wystąpienie
- G: koniec pliku
- g: początek pliku

Przykład:
less /var/log/messages
cat duzy_plik.txt | less
```

## 8. Wyświetlanie zawartości pliku wraz z podkreśleniem wyszukiwanego słowa kluczowego

```
Grep z kolorowaniem:
grep --color=always "słowo" plik.txt

Cat z grep:
cat plik.txt | grep --color=always "wzorzec"

Less z wyszukiwaniem:
less plik.txt
# Następnie /słowo w less

Highlighter z grep:
grep --color=always -E "błąd|error|fail" /var/log/messages

Przykłady:
cat /var/log/messages | grep --color=always "error"
grep --color=always "root" /etc/passwd
cat plik.txt | grep --color=always -i "ważne"  # Bez wielkości liter
```

## 9. Wyświetlanie zawartości pliku z pominięciem powtarzających się linii

```
Uniq (wymaga sortowania):
sort plik.txt | uniq

Cat z sort i uniq:
cat plik.txt | sort | uniq

Tylko unikalne linie:
sort plik.txt | uniq -u

Tylko powtarzające się linie:
sort plik.txt | uniq -d

Liczenie wystąpień:
sort plik.txt | uniq -c

Przykłady:
cat /etc/passwd | cut -d: -f7 | sort | uniq  # Unikalne shelle
cat access.log | awk '{print $1}' | sort | uniq -c  # IP i liczba wystąpień
```

## 10. Przeglądanie zawartości pliku z paginacją

```
Less (najlepszy):
less plik.txt

More:
more plik.txt

Cat z piperowaniem:
cat plik.txt | less

Most (jeśli zainstalowany):
most plik.txt

Funkcje less:
- Przewijanie w górę i w dół
- Wyszukiwanie (/)
- Skakanie do linii (:numer)
- Oznaczanie (m + litera)
- Podział ekranu (s)

Przykład:
less /var/log/messages
less +F /var/log/messages  # Tryb follow (jak tail -f)
```

## 11. Przeglądanie pliku w trybie tylko do odczytu, uniemożliwiając zmiany

```
View (vim w trybie readonly):
view plik.txt

Less (zawsze readonly):
less plik.txt

Vim w trybie readonly:
vim -R plik.txt

Cat (zawsze readonly):
cat plik.txt

Readonly przez uprawnienia:
chmod 444 plik.txt
cat plik.txt

Przykłady:
view /etc/passwd
less /etc/shadow
vim -R ~/.bashrc
```

## 12. Przeglądanie pliku od ostatniej linii

```
Tail:
tail plik.txt

Tail z follow:
tail -f plik.txt

Less z końcem:
less +G plik.txt

Tail z określoną liczbą linii:
tail -20 plik.txt

Przykłady:
tail -f /var/log/messages     # Podąża za zmianami
tail -100 /var/log/apache2/access.log
less +G ~/.bash_history       # Otwiera na końcu
```

## 13. Przeszukiwanie pliku w poszukiwaniu określonego wyrażenia

```
Grep:
grep "wzorzec" plik.txt

Grep z numerami linii:
grep -n "wzorzec" plik.txt

Grep bez wielkości liter:
grep -i "wzorzec" plik.txt

Cat z grep:
cat plik.txt | grep "wzorzec"

Zaawansowane wyszukiwanie:
grep -E "wzorzec1|wzorzec2" plik.txt
grep -r "wzorzec" katalog/
grep -B 3 -A 3 "wzorzec" plik.txt  # Kontekst

Przykłady:
grep "error" /var/log/messages
grep -n "root" /etc/passwd
grep -i "warning" *.log
grep -r "TODO" ~/projekt/
```

## 14. Wyświetlanie numerowanych linii w pliku

```
Cat z numerowaniem:
cat -n plik.txt

Numerowanie tylko niepustych linii:
cat -b plik.txt

Nl (number lines):
nl plik.txt

Grep z numerami linii:
grep -n ".*" plik.txt

Awk z numerowaniem:
awk '{print NR ": " $0}' plik.txt

Przykłady:
cat -n /etc/passwd
cat -b ~/.bashrc  # Pomija puste linie
nl /etc/hosts
less -N plik.txt  # W less z numerami

Różne style numerowania:
nl -s ": " plik.txt     # Separator
nl -w 3 plik.txt        # Szerokość numeru
nl -v 10 plik.txt       # Zacznij od 10
```

## Dodatkowe przydatne polecenia cat

```
Wyświetlanie nieprintable characters:
cat -A plik.txt

Pokazywanie końców linii:
cat -E plik.txt

Pokazywanie tabów:
cat -T plik.txt

Łączenie z innymi poleceniami:
cat plik.txt | wc -l     # Liczba linii
cat plik.txt | sort      # Sortowanie
cat plik.txt | tr '[:lower:]' '[:upper:]'  # Wielkie litery

Tworzenie pliku z cat:
cat > nowy_plik.txt << EOF
Linia 1
Linia 2
EOF

Kopiowanie z cat:
cat źródło.txt > cel.txt

Here documents:
cat << EOF > plik.txt
Zawartość
pliku
EOF
```