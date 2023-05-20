1.  Przejrzyj plik konfiguracyjny i sprawdź jakie ma opcje /etc/default/grub
```
cat /etc/default/grub
```

2.  Sprawdź pliki znajdujące się na partycji /boot, co tam możesz znaleźć?
```
cd /boot
ls /boot
```

3.  Użyj polecenia rpm, aby stworzyć listę wszystkich zainstalowanych kerneli w twoim systemie. 
```
rpm -qa | grep kernel
```

4.  Sprawdź wersję jądra, która jest aktualnie uruchomiona.
```
cat /proc/version
uname -r
```

5. Sprawdź listę aktualnie załadowanych modułów.
```
lsmod
```