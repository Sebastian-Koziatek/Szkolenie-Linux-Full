# Rozwiązania - Find i locate

## 1. Znajdź wszystkie pliki z rozszerzeniem .txt w bieżącym katalogu i jego podkatalogach.

```
Polecenie:
find . -name "*.txt"

Wyjaśnienie:
- . = bieżący katalog
- -name = wyszukiwanie po nazwie
- "*.txt" = wzorzec z wildcards

Alternatywne wersje:
find . -type f -name "*.txt"     # Tylko pliki (nie katalogi)
find . -iname "*.txt"            # Bez wielkości liter
find . -name "*.txt" -type f     # Identyczne z pierwszą alternatywą

Przykłady:
find /home/user -name "*.txt"
find . -name "dokument*.txt"
find . -name "*raport*.txt"
```

## 2. Znajdź pliki, które zostały zmodyfikowane w ciągu ostatnich 7 dni w katalogu /home/user.

```
Polecenie:
find /home/user -mtime -7

Wyjaśnienie:
- -mtime = modification time
- -7 = mniej niż 7 dni temu (ostatnie 7 dni)
- +7 = więcej niż 7 dni temu

Alternatywy:
find /home/user -mtime -7 -type f    # Tylko pliki
find /home/user -newermt "7 days ago" # Nowsza składnia
find /home/user -mtime -7 -ls        # Z szczegółami

Inne opcje czasu:
-atime = access time (ostatni dostęp)
-ctime = change time (zmiana metadanych)
-mmin = minuty zamiast dni

Przykłady:
find /home/user -mtime -1    # Ostatni dzień
find /home/user -mtime +30   # Starsze niż 30 dni
find /home/user -mmin -60    # Ostatnia godzina
```

## 3. Znajdź pliki, które mają rozmiar większy niż 1 MB w katalogu /var/log.

```
Polecenie:
find /var/log -size +1M

Wyjaśnienie:
- -size = rozmiar pliku
- +1M = większy niż 1 megabajt
- M = megabajty

Jednostki rozmiaru:
c = bajty
k = kilobajty  
M = megabajty
G = gigabajty

Alternatywy:
find /var/log -size +1M -type f       # Tylko pliki
find /var/log -size +1M -ls           # Z szczegółami
find /var/log -size +1048576c         # W bajtach (1MB = 1048576 bajtów)

Przykłady zakresów:
find /var/log -size +1M -size -10M    # Między 1MB a 10MB
find /var/log -size +100k             # Większe niż 100KB
find /var/log -size 1M                # Dokładnie 1MB
find /var/log -size -1M               # Mniejsze niż 1MB
```

## 4. Znajdź wszystkie pliki, które należą do użytkownika john w całym systemie.

```
Polecenie:
find / -user john

Wyjaśnienie:
- / = cały system (root directory)
- -user = właściciel pliku

Dodatkowe opcje:
find / -user john -type f            # Tylko pliki
find / -user john 2>/dev/null        # Bez błędów "Permission denied"
sudo find / -user john               # Z uprawnieniami root

Wyszukiwanie po grupie:
find / -group john                   # Pliki należące do grupy john
find / -user john -group users       # Określony user i grupa

Wyszukiwanie po UID/GID:
find / -uid 1001                     # Po numerze UID
find / -gid 1001                     # Po numerze GID

Przykłady:
find /home -user john
find /tmp -user john -type f
find / -user john -name "*.txt" 2>/dev/null
```

## 5. Znajdź wszystkie katalogi, które mają nazwę "test" w swojej ścieżce.

```
Polecenie:
find / -type d -name "*test*"

Wyjaśnienie:
- -type d = tylko katalogi (directories)
- -name "*test*" = nazwa zawiera "test"

Alternatywy:
find / -type d -iname "*test*"       # Bez wielkości liter
find / -type d -path "*test*"        # W pełnej ścieżce
find / -type d -name "test"          # Dokładnie "test"

Różne wzorce:
find / -type d -name "test*"         # Zaczyna się od "test"
find / -type d -name "*test"         # Kończy się na "test"
find / -type d -regex ".*test.*"     # Wyrażenia regularne

Przykłady:
find /home -type d -name "*test*"
find /var -type d -iname "*TEST*"
find . -type d -name "test_*"
```

## 6. Znajdź pliki wykonywalne w katalogu /bin.

```
Polecenie:
find /usr/bin -type f -executable

Wyjaśnienie:
- -type f = tylko pliki
- -executable = pliki wykonywalne

Alternatywy:
find /usr/bin -type f -perm /111      # Uprawnienia execute dla kogokolwiek
find /usr/bin -type f -perm -111      # Execute dla wszystkich (owner,group,other)
find /usr/bin -type f -perm 755       # Konkretne uprawnienia

Różne formaty uprawnień:
-perm 755        # Dokładnie 755
-perm -755       # Minimum 755
-perm /755       # Którykolwiek bit z 755

Przykłady:
find /usr/bin -name "*ssh*" -executable
find /bin -type f -executable | head -10
find /usr/local/bin -perm /111
```

## 7. Znajdź pliki o nazwie "config" bez względu na wielkość liter w katalogu /etc.

```
Polecenie:
find /etc -iname "config"

Wyjaśnienie:
- -iname = case-insensitive name search
- Znajdzie: config, Config, CONFIG, cOnFiG

Alternatywy:
find /etc -iname "*config*"          # Zawiera "config"
find /etc -type f -iname "config"    # Tylko pliki
find /etc -iname "config*"           # Zaczyna się od "config"

Różne wzorce:
find /etc -iname "*.conf"            # Pliki konfiguracyjne
find /etc -iname "*config*.conf"     # Config files z config w nazwie
find /etc -regex "(?i).*config.*"    # Regex case-insensitive

Przykłady:
find /etc -iname "*apache*"
find /etc -type f -iname "*.conf"
find /etc -iname "ssh*"
```

## 8. Znajdź pliki, które zawierają określone słowo kluczowe "error" w katalogu /var/log.

```
Polecenie:
find /var/log -type f -exec grep -l "error" {} +

Wyjaśnienie:
- -type f = tylko pliki
- -exec = wykonaj polecenie
- grep -l = tylko nazwy plików zawierających wzorzec
- {} = placeholder dla znalezionego pliku
- + = grupuj argumenty (wydajniejsze niż \;)

Alternatywy:
find /var/log -type f -exec grep -l "error" {} \;
find /var/log -name "*.log" -exec grep -l "error" {} +
grep -r "error" /var/log                              # Rekurencyjny grep

Dodatkowe opcje grep:
find /var/log -type f -exec grep -il "error" {} +    # Case insensitive
find /var/log -type f -exec grep -c "error" {} +     # Liczba wystąpień
find /var/log -type f -exec grep -H "error" {} +     # Z nazwami plików

Przykłady:
find /var/log -name "*.log" -exec grep -l "failed" {} +
find /var/log -type f -exec grep -l "warning\|error" {} +
find . -name "*.txt" -exec grep -l "TODO" {} +
```

## 9. Znajdź wszystkie pliki, które nie zostały zmodyfikowane w ciągu ostatnich 30 dni w katalogu /home/user/docs.

```
Polecenie:
find /home/user/docs -type f -mtime +30

Wyjaśnienie:
- -type f = tylko pliki
- -mtime +30 = starsze niż 30 dni
- + oznacza "więcej niż"

Alternatywy:
find /home/user/docs -mtime +30 -type f
find /home/user/docs -not -mtime -30 -type f
find /home/user/docs -mtime +30 -ls

Kombinacje:
find /home/user/docs -type f -mtime +30 -size +1M    # Stare i duże
find /home/user/docs -type f -mtime +30 -name "*.tmp" # Stare pliki tmp

Inne opcje czasu:
find /home/user/docs -atime +30     # Nie dostępne przez 30 dni
find /home/user/docs -ctime +30     # Metadane nie zmieniane 30 dni

Przykłady:
find /home/user/docs -mtime +90     # Starsze niż 3 miesiące
find /tmp -mtime +7 -type f         # Stare pliki tymczasowe
```

## 10. Znajdź wszystkie pliki, które mają ustawione prawa dostępu 777 w katalogu /var/www.

```
Polecenie:
find /var/www -type f -perm 777

Wyjaśnienie:
- -perm 777 = dokładnie uprawnienia 777 (rwxrwxrwx)
- 777 = read,write,execute dla all (owner,group,other)

Alternatywy:
find /var/www -perm 777             # Pliki i katalogi
find /var/www -type f -perm -777    # Minimum 777
find /var/www -type f -perm /777    # Dowolny bit z 777

Inne niebezpieczne uprawnienia:
find /var/www -type f -perm 666     # rw-rw-rw-
find /var/www -type f -perm /002    # Writeable by others
find /var/www -type f -perm /022    # Writeable by group or others

Wyszukiwanie SUID/SGID:
find /var/www -type f -perm /4000   # SUID files
find /var/www -type f -perm /2000   # SGID files

Przykłady:
find /var/www -perm 777 -ls
find /home -type f -perm 644
find /usr/bin -type f -perm /4000   # SUID binaries
```

## 11. Znajdź pliki, które są większe niż 100 MB i zostały zmodyfikowane w ciągu ostatnich 60 dni w katalogu /home/user/files.

```
Polecenie:
find /home/user/files -type f -size +100M -mtime -60

Wyjaśnienie:
- Łączenie dwóch warunków: rozmiar AND czas modyfikacji
- -size +100M = większe niż 100MB
- -mtime -60 = ostatnie 60 dni

Alternatywy:
find /home/user/files -size +100M -mtime -60 -type f
find /home/user/files -size +100M -mtime -60 -ls

Różne kombinacje:
find /home/user/files -size +100M -mtime -60 -name "*.mp4"
find /home/user/files -size +50M -size -200M -mtime -30

Dodanie akcji:
find /home/user/files -size +100M -mtime -60 -exec ls -lh {} \;
find /home/user/files -size +100M -mtime -60 -print0 | xargs -0 du -h

Przykłady zastosowań:
# Znajdź duże logi z ostatniego miesiąca
find /var/log -size +10M -mtime -30
# Znajdź duże pliki multimedialne
find ~/Downloads -size +500M -name "*.mp4" -mtime -7
```

## 12. Znajdź pliki, które mają rozszerzenie .log i zawierają słowo kluczowe "failed" w katalogu /var/log.

```
Polecenie:
find /var/log -type f -name "*.log" -exec grep -l "failed" {} +

Wyjaśnienie:
- -name "*.log" = tylko pliki .log
- -exec grep -l "failed" {} + = grep w znalezionych plikach

Alternatywy:
find /var/log -name "*.log" -exec grep -l "failed" {} \;
find /var/log -name "*.log" | xargs grep -l "failed"

Dodatkowe opcje:
find /var/log -name "*.log" -exec grep -il "failed" {} +     # Case insensitive
find /var/log -name "*.log" -exec grep -c "failed" {} +      # Count occurrences
find /var/log -name "*.log" -exec grep -H "failed" {} +      # Show filenames

Różne wzorce:
find /var/log -name "*.log" -exec grep -E "failed|error" {} +
find /var/log -name "*error*.log" -exec grep -l "failed" {} +

Przykłady:
find /var/log -name "*.log" -exec grep -l "authentication failure" {} +
find . -name "*.log" -exec grep -l "CRITICAL" {} +
```

## 13. Znajdź pliki, które zostały utworzone w ciągu ostatnich 24 godzin w katalogu /tmp.

```
Polecenie:
find /tmp -type f -ctime 0

Wyjaśnienie:
- -ctime 0 = zmienione w ciągu ostatnich 24 godzin
- ctime = change time (creation/metadata change)

Alternatywy:
find /tmp -type f -newerct "1 day ago"
find /tmp -type f -cmin -1440           # Ostatnie 1440 minut (24h)
find /tmp -type f -newer /tmp/reference_file

Różne opcje czasu:
-mtime 0    # Modified w ostatnich 24h
-atime 0    # Accessed w ostatnich 24h
-ctime 0    # Changed w ostatnich 24h

Dokładniejsze opcje:
find /tmp -type f -newerct "yesterday"
find /tmp -type f -newerct "2023-10-23"
find /tmp -type f -newerct "2023-10-23 10:00"

Przykłady:
find /tmp -type f -ctime 0 -user $(whoami)
find /var/log -name "*.log" -mtime 0
find ~/Downloads -type f -ctime 0
```

## 14. Znajdź wszystkie pliki, które nie są własnością bieżącego użytkownika w katalogu /home.

```
Polecenie:
find /home ! -user "$(whoami)"

Wyjaśnienie:
- ! = negacja (NOT)
- $(whoami) = aktualny użytkownik
- Znajdzie pliki należące do innych użytkowników

Alternatywy:
find /home -not -user "$(whoami)"
find /home ! -user $USER
find /home ! -uid $(id -u)

Dodatkowe filtry:
find /home ! -user "$(whoami)" -type f           # Tylko pliki
find /home ! -user "$(whoami)" ! -user root      # Nie current user i nie root

Kombinacje:
find /home ! -user "$(whoami)" -executable       # Nie moje executable
find /home ! -user "$(whoami)" -perm /002        # Nie moje ale writeable

Przykłady praktyczne:
find /home ! -user "$(whoami)" -ls
find /tmp ! -user "$(whoami)" -type f
find /var/www ! -user www-data
```

## 15. Znajdź pliki, które są symlinkami do określonego katalogu /opt/app w całym systemie.

```
Polecenie:
find / -type l -lname "/opt/app/*"

Wyjaśnienie:
- -type l = symbolic links
- -lname = target of symbolic link
- "/opt/app/*" = wzorzec dla targetu

Alternatywy:
find / -type l -lname "/opt/app*"              # Rozpoczyna się od /opt/app
find / -type l | xargs ls -la | grep "/opt/app"

Sprawdzanie wszystkich symlinków:
find / -type l -ls                             # Wszystkie symlinki
find / -type l -exec ls -la {} \;              # Z targetami

Broken symlinks:
find / -type l ! -exec test -e {} \; -print    # Zepsute symlinki

Przykłady:
find /usr/bin -type l -lname "/opt/app/*"
find /etc -type l -lname "/opt/app/config/*"
find / -type l -lname "*/opt/app*" 2>/dev/null
```

## Dodatkowe przydatne opcje find

```
Wykonywanie akcji:
-exec command {} \;        # Pojedyncze wykonanie
-exec command {} +         # Grupowe wykonanie (wydajniejsze)
-delete                    # Usuń znalezione pliki
-print0                    # Null-separated output

Kombinowanie warunków:
-a, -and                   # AND (domyślne)
-o, -or                    # OR
! , -not                   # NOT
\( ... \)                  # Grupowanie

Przykłady zaawansowane:
find . \( -name "*.tmp" -o -name "*.cache" \) -mtime +7 -delete
find . -type f -size +100M -exec du -h {} \; | sort -hr
find /var/log -name "*.log" -mtime +30 -exec gzip {} \;

Performance tips:
- Używaj -type na początku
- Używaj -path zamiast -name dla ścieżek
- Używaj -exec ... + zamiast -exec ... \;
- Używaj -maxdepth aby ograniczyć głębokość
```