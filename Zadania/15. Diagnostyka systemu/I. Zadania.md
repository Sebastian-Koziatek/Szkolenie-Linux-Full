1.  Znajdz 3 największe pod względem rozmiaru pliki w systemie
    1.  `du -a / | sort -n -r | head -n 3`
2.  Sprawdź jakie 5 procesów najbardziej obciąża ram
    1.  top / htop
3.  Sprawdź jakie 5 procesów najbardziej obciąża CPU
    1.  `ps aux | sort -nrk 3,3 | head -n 5`
    2.  top / htop
4.  Sprawdź ile masz wolnego miejsca ram na komputerze
    1.  free -m
5.  Sprawdź ile pamięci SWAP jest używane
    1.  free -m
6.  Wyłącz pamięć swap i włącz ponownie
    1.  sudo swapoff -a
    2.  sudo swapon -a
7.  Sprawdź jacy użytkownicy są podłączeniu do systemu
    1.  w
8.  Sprawdź jak długo system jest uruchomiony
    1.  uptime
9.  Sprawdź nazwę serwerwa
    1.  hostname
10.  Wylistuj wszystkie procesy używane przez swojego użytkownika
    1.  ps -u sebkoz
11.  Sprawdź jakie PID posiada proces sshd
    1.  ps aux | grep sshd
12.  Sprawdź zajętość dysków twardych, ile twój dysk ma wolnego miejsca dla partycji root?
    1.  df -h
13.  Sprawdź jakie porty masz odblokowane
    1.  sudo nmap 192.168.10.30
14.  Zczytaj bezpośrednio z kernela informacje o:
    1.  CPU
        1.  `cat /proc/cpuinfo`
    2.  Pamięci
        1.  **cat /proc/meminfo**
15.  Sprawdź jakie opóźnienia masz łącząc się z adresem np. [wp.pl](http://wp.pl)
    1.  ping [wp.pl](http://wp.pl)
16.  Sprawdz listę uruchomionych w systemie serwisów
    1.  `systemctl list-units --type=service`
17.  Sprwadź tabelę routingu
    1.  route
18.  Zainstaluj i uruchom polecenie **lsof - przejrzyj podane informacje**