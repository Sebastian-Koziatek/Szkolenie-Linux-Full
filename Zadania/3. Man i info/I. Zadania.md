1. **Użyj polecenia `man man` i zapoznaj się ze strukturą stron podręcznika (`man pages`).**  
   - Zwróć uwagę na sekcje: NAME, SYNOPSIS, DESCRIPTION, EXAMPLES itd.  
   - Jakie informacje można znaleźć w każdej z nich?

2. **Przejrzyj stronę podręcznika dla polecenia `ls`.**  
   ```
   man ls
   ```
   - Do której sekcji należy polecenie `ls`?  
   - Jakie opcje `ls` pozwalają na sortowanie wyników?  
   - Wypisz przynajmniej 3 przydatne przełączniki.

3. **Zainstaluj pakiet `info` i przejrzyj strukturę dokumentacji `info` dla polecenia `pwd`.**  
   ```
   sudo dnf install info   # lub sudo yum install info
   info pwd
   ```
   - Jak wygląda struktura dokumentacji w `info` w porównaniu do `man`?  
   - Jakie są różnice w nawigacji między `man` a `info`?

4. **Zainstaluj pakiet `mc` (Midnight Commander) i sprawdź, czy dostępna jest dokumentacja w `man` i `info`.**  
   ```
   sudo yum install mc
   man mc
   info mc
   ```
   - Czy `mc` posiada własną stronę podręcznika?  
   - Czy dostępna jest dokumentacja `info`? Jeśli nie – jakie mogą być przyczyny?  
   - Jak uruchomić wbudowaną pomoc w samym `mc`?

