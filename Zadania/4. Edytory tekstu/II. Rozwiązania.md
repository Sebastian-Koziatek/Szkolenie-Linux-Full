1. Stwórz za pomocą edytora tekstu plik "temp.txt" 

```
vi temp.txt
```

2. Napisz w tym pliku frazę "Szkolenie Linux" 
```
i
Szkolenie linux
```

3. Zapisz plik i wyjdź z edytora. 
```
ESC
:wq
ENTER
```

4. Otwórz plik "temp.txt" z pomocą edytora VI
```
vi temp.txt
```

5. Dopiszę frazę po "Szkolenie Linux" o treści "jest proste" (użyj do tego poprawnego skrótu klawiszowego) (duże A)


6. Wyjdź z pliku bez zapisywania 
```
ESC 
:q!
ENTER
```

7. Ściągnij Pana Tadeusza w wersji txt przy użyciu polecenia "wget" 
```
wget https://wolnelektury.pl/media/book/txt/pan-tadeusz.txt
```

8. Uruchom ściągniętą książkę za pomocą edytora vi 
```
vi pan-tadeusz.txt
```

9. Wyszukaj imię bohatera tytułowego i przeszukaj powtórzenia frazy. 
```
/
Tadeusz
/
Tadeusz
/
Tadeusz
```

10. Uruchom plik pan-tadeusz.txt za pomocą edytora nano 
```
nano pan-tadeusz.txt
```

11. Wyszukaj frazę "Tadeusz" i poszukaj kolejnych wystąpień frazy. 
```
ctrl + w
Tadeusz

Kolejne wystąpienie w tekście
alt + w

Poprzednie wystąpienie w tekście
alt + q
```

12. Wyjdź z edytora bez zapisywania
```
ctrl + x 
n
ENTER
```

13. Otwórz plik temp.txt za pomocą edytora nano 
```
nano temp.txt
```

14. Skasuj cały wiersz przy użyciu odpowiedniego skrótu 
```
ctrl + k
```

15. Wprowadź do pliku frazę "Używam edytora nano" 
16. Zapisz plik i wyjdź z edytora.   
```
ctrl + x 
y
ENTER
```
