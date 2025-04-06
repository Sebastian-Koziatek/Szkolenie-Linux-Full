# Dzień 5 – Odpowiedzi: Podstawy pracy w powłoce

1. **Sprawdź, w jakim katalogu aktualnie się znajdujesz:**  
   ```bash
   pwd
   ```

2. **Wyświetl zawartość bieżącego katalogu:**  
   ```bash
   ls
   ```

3. **Utwórz nowy katalog o nazwie `szkolenie`:**  
   ```bash
   mkdir szkolenie
   ```

4. **Przejdź do katalogu `szkolenie`:**  
   ```bash
   cd szkolenie
   ```

5. **Utwórz pięć plików za pomocą jednego polecenia:**  
   ```bash
   touch plik1 plik2 plik3 plik4 plik5
   ```

6. **Utwórz ukryty plik `.ukryty.txt`:**  
   ```bash
   touch .ukryty.txt
   ```

7. **Wyświetl pełną zawartość katalogu, łącznie z ukrytymi plikami:**  
   ```bash
   ls -la
   ```

8. **Zmień nazwę `.ukryty.txt` na `plik6`:**  
   ```bash
   mv .ukryty.txt plik6
   ```

9. **Zapisz tekst „Szkolenie Linux” do pliku `plik3`:**  
   ```bash
   echo "Szkolenie Linux" > plik3
   ```

10. **Wyświetl zawartość pliku `plik3`:**  
    ```bash
    cat plik3
    ```

11. **Utwórz folder `/tmp/test`:**  
    ```bash
    mkdir /tmp/test
    ```

12. **Opis katalogu `/tmp`:**  
    - Tymczasowy katalog przeznaczony na pliki sesyjne i tymczasowe.  
    - Dostępny dla każdego użytkownika.  
    - Zawartość zwykle usuwana jest przy restarcie systemu.

13. **Skopiuj zawartość bieżącego katalogu do `/tmp/test`:**  
    ```bash
    cp * /tmp/test/
    ```

14. **Wyświetl zawartość katalogu `/tmp/test`:**  
    ```bash
    ls /tmp/test
    ```

15. **Przejdź jeden katalog wyżej:**  
    ```bash
    cd ..
    ```

16. **Wyświetl zawartość `/tmp`, pokazując tylko katalog `test`:**  
    ```bash
    ls -d /tmp/test
    ```

17. **Usuń wszystkie pliki w katalogu `/tmp/test`:**  
    ```bash
    rm /tmp/test/*
    ```

18. **Wróć katalog wyżej:**  
    ```bash
    cd ..
    ```

19. **Usuń folder `test`:**  
    ```bash
    rmdir /tmp/test
    ```
    *lub jeśli nie jest pusty:*  
    ```bash
    rm -r /tmp/test
    ```

20. **Wróć do katalogu domowego użytkownika:**  
    ```bash
    cd ~
    ```

21. **Wyświetl historię ostatnio używanych poleceń:**  
    ```bash
    history
    ```

22. **Zapisz historię poleceń do pliku `historia.txt`:**  
    ```bash
    history > historia.txt
    ```
