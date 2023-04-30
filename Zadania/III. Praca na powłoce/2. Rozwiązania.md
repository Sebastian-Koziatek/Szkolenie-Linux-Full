1. **Sprawdź w jakim katalogu jesteś.**
```
pwd
```

2. **Wyświetl zwartość tego katalogu.**
```
ls
```

3. **Stwórz nowy katalog o nazwie "szkolenie" w lokalizacji w której się znajdujesz.**
```
mkdir szkolenie
```

4. **Przejdź do katalogu "szkolenie".**
```
cd szkolenie
```

5. **Stwórz w ramach 1 polecenia 5 plików o nazwie "plik1", "plik2", "plik3", "plik4", "plik5"**
```
touch plik1 plik2 plik3 plik4 plik5
```

6. Stwórz "ukryty" plik o nazwie ukryty.txt
```
touch .ukryty.txt
```
  
7. Wyświetl pełną listę katalogów i plików w miejscu w którym się znajdujesz.
```
ls -la
```

8. Zmień nazwę pliku ukryty.txt na "plik6"
```
mv .ukryty.txt plik6
```
  
9. Wprowadź z linii wiersza poleceń frazę "Szkolenie linux" do pliku "plik3"
```
echo “Szkolenie linux” > plik3
```

10. Wyświetli zawartość pliku "plik3".
```
cat plik3
```
  
11. Z lokalizacji w której jesteś stwórz folder w katalogu /tmp i nazwij go "test"
```
mkdir /tmp/test
```
  
12. Czym jest katalog /tmp i jakie ma wlaściwości?
```
Przechowuje pliki tymczasowe i czysci sie na starcie systemu
```

13. Skopiuj zawartość aktualnego folderu do katalogu /tmp/test
```
cp * /tmp/test
```

14. Z lokalizacji w której jesteś wyświetl zawartośc katalogu /tmp/test
```
ls /tmp/test
```
  
  15. Przejdz do katalogu poziom wyzej
```
cd ../
```
  
16. W do katalogu /tmp wyświetl listę plików i folderów która pokaze tylko folder 'test'
```
ls | grep test
```
  
17. Wejdz do katalogu test i skasuj wszystkie pliki
```
cd test
rm -rf *
```
  
18. Przejdz do katalogu wyzej
```
cd ../
```
  
19. Skasuj folder 'test"
```
rm -rf test
```

20. Wróc do katalogu domowego swojego uzytkownika
```
cd ~/.
cd /home/user
```

21. Wyświetl historie wykonanych polecen
```  
history
```

22. Zapisz historie polecen do pliku historia.txt
```
history > historia.txt
```

  

