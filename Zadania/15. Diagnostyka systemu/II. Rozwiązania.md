## Rozwiązania – Diagnostyka systemu

1. **Znajdź 3 największe pod względem rozmiaru pliki w systemie:**
```bash
sudo find / -type f -exec du -h {} + 2>/dev/null | sort -hr | head -n 3
```

2. **Sprawdź jakie 5 procesów najbardziej obciąża RAM:**
```bash
ps aux --sort=-%mem | head -n 6
```

3. **Sprawdź jakie 5 procesów najbardziej obciąża CPU:**
```bash
ps aux --sort=-%cpu | head -n 6
```

4. **Sprawdź ile masz wolnego miejsca RAM na komputerze:**
```bash
free -h
```

5. **Sprawdź ile pamięci SWAP jest używane:**
```bash
free -h | grep Swap
```

6. **Wyłącz pamięć swap i włącz ponownie:**
```bash
sudo swapoff -a
sudo swapon -a
```

7. **Sprawdź jacy użytkownicy są podłączeni do systemu:**
```bash
who
```

8. **Sprawdź jak długo system jest uruchomiony:**
```bash
uptime
```

9. **Sprawdź nazwę serwera:**
```bash
hostname
```

10. **Wylistuj wszystkie procesy używane przez swojego użytkownika:**
```bash
ps -u $(whoami)
```

11. **Sprawdź jakie PID posiada proces sshd:**
```bash
pgrep sshd
```

12. **Sprawdź zajętość dysków twardych, ile twój dysk ma wolnego miejsca dla partycji root?:**
```bash
df -h /
```

13. **Sprawdź jakie porty masz odblokowane:**
```bash
sudo ss -tuln
```

14. **Zczytaj bezpośrednio z kernela informacje o:**
(np. wersja kernela)
```bash
uname -a
```

15. **Sprawdź jakie opóźnienia masz łącząc się z adresem np. wp.pl:**
```bash
ping -c 4 wp.pl
```

16. **Sprawdź listę uruchomionych w systemie serwisów:**
```bash
systemctl list-units --type=service --state=running
```

17. **Sprawdź tabelę routingu:**
```bash
ip route
```

18. **Zainstaluj i uruchom polecenie lsof – przejrzyj podane informacje:**
```bash
sudo dnf install lsof
lsof
```
