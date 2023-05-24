1. Znajdź wszystkie pliki z rozszerzeniem .txt w bieżącym katalogu i jego podkatalogach.
```
find . -name "*.txt"
```

2. Znajdź pliki, które zostały zmodyfikowane w ciągu ostatnich 7 dni w katalogu /home/user.
```
find /home/user -mtime -7
```

2. Znajdź pliki, które mają rozmiar większy niż 1 MB w katalogu /var/log.
```
find /var/log -size +1M
```

3. Znajdź wszystkie pliki, które należą do użytkownika john w całym systemie.
```
find / -user john
```

4. Znajdź wszystkie katalogi, które mają nazwę "test" w swojej ścieżce.
```
find / -type d -name "*test*"
```

5. Znajdź pliki wykonywalne w katalogu /bin.
```
find /bin -type f -executable
```

6. Znajdź pliki o nazwie "config" bez względu na wielkość liter w katalogu /etc.
```
find /etc -iname "config"
```

7. Znajdź pliki, które zawierają określone słowo kluczowe "error" w katalogu /var/log.
```
find /var/log -type f -exec grep -l "error" {} +
```

8. Znajdź wszystkie pliki, które nie zostały zmodyfikowane w ciągu ostatnich 30 dni w katalogu /home/user/docs.
```
find /home/user/docs -type f -mtime +3
```

9. Znajdź wszystkie pliki, które mają ustawione prawa dostępu 777 w katalogu /var/www.
```
find /var/www -type f -perm 777
```

10. Znajdź pliki, które są większe niż 100 MB i zostały zmodyfikowane w ciągu ostatnich 60 dni w katalogu /home/user/files.
```
find /home/user/files -type f -size +100M -mtime -60
```

11. Znajdź pliki, które mają rozszerzenie .log i zawierają słowo kluczowe "failed" w katalogu /var/log.
```
find /var/log -type f -name "*.log" -exec grep -l "failed" {} +
```

12. Znajdź pliki, które zostały utworzone w ciągu ostatnich 24 godzin w katalogu /tmp.
```
find /tmp -type f -ctime 0
```

13. Znajdź wszystkie pliki, które nie są własnością bieżącego użytkownika w katalogu /home.
```
find /home ! -user "$(whoami)"
```

14. Znajdź pliki, które są symlinkami do określonego katalogu /opt/app w całym systemie.
```
find / -type l -lname "/opt/app/*"
```
