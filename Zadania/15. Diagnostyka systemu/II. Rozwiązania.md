1.  Znajdz 3 największe pod względem rozmiaru pliki w systemie
```
du -a / | sort -n -r | head -n 3
```

2. Sprawdź jakie 5 procesów najbardziej obciąża ram
```
top / htop
```

 3. Sprawdź jakie 5 procesów najbardziej obciąża CPU
```
ps aux | sort -nrk 3,3 | head -n 5`
top / htop
```

  4. Sprawdź ile masz wolnego miejsca ram na komputerze
```
free -m
```

 5. Sprawdź ile pamięci SWAP jest używane
```
 free -m
```

6. Wyłącz pamięć swap i włącz ponownie
```
sudo swapoff -a
sudo swapon -a
```
7. Sprawdź jacy użytkownicy są podłączeniu do systemu
```
w
```

8.  Sprawdź jak długo system jest uruchomiony
```
 uptime
```

 9. Sprawdź nazwę serwerwa
```
hostname
```

10.  Wylistuj wszystkie procesy używane przez swojego użytkownika
```
 ps -u sebkoz
```

11. Sprawdź jakie PID posiada proces sshd
```
ps aux | grep sshd
```

12. Sprawdź zajętość dysków twardych, ile twój dysk ma wolnego miejsca dla partycji root?
```
df -h
```

13.  Sprawdź jakie porty masz odblokowane
```
 sudo nmap 192.168.10.30
```

14.  Zczytaj bezpośrednio z kernela informacje o:
- CPU
```
cat /proc/cpuinfo
```
- Pamięci
```
 cat /proc/meminfo
```

15. Sprawdź jakie opóźnienia masz łącząc się z adresem np. [wp.pl](http://wp.pl)
```
ping wp.pl
```

16. Sprawdz listę uruchomionych w systemie serwisów
```
systemctl list-units --type=service
```

17. Sprwadź tabelę routingu
```
route
```

18.  Zainstaluj i uruchom polecenie **lsof - przejrzyj podane informacje**