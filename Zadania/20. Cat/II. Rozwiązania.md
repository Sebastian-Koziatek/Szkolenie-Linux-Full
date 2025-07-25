1. Wyświetlanie zawartości pliku na ekranie:``
```
cat nazwa_pliku
```

2. Wyświetlanie zawartości wielu plików jednocześnie:
```
cat plik1 plik2 plik3
```

3. Łączenie zawartości kilku plików i zapisywanie ich do nowego pliku:
```
cat plik1 plik2 > nowy_plik
```

4. Wyświetlanie numerowanych linii w pliku:
```
cat -n nazwa_pliku
```

5. Wyświetlanie zawartości pliku w odwróconej kolejności:
```
tac nazwa_pliku
```

6. Wyświetlanie tylko określonej liczby linii pliku:
```
cat nazwa_pliku | head -n 10
```

7. Wyświetlanie zawartości pliku z paginacją (pozwala na przewijanie strony po stronie):
```
cat nazwa_pliku | less
```

8. Wyświetlanie zawartości pliku wraz z podkreśleniem wyszukiwanego słowa kluczowego:
```
cat nazwa_pliku | grep "słowo"
```

9. Wyświetlanie zawartości pliku z pominięciem powtarzających się linii:
```
cat nazwa_pliku | uniq
```

10. Przeglądanie zawartości pliku z paginacją (pozwala na przewijanie strony po stronie):
```
less nazwa_pliku
```

11. Przeglądanie pliku w trybie tylko do odczytu, uniemożliwiając zmiany:
```
less -r nazwa_pliku
```

12. Przeglądanie pliku od ostatniej linii:
```
less +G nazwa_pliku
```

13. Przeszukiwanie pliku w poszukiwaniu określonego wyrażenia:
```
less nazwa_pliku
n   # Przejdź do następnego wystąpienia wyrażenia
N   # Przejdź do poprzedniego wystąpienia wyrażenia
```

14. Wyświetlanie numerowanych linii w pliku:
```
less -N nazwa_pliku
```
