# Dzień 3 – Odpowiedzi: `man` i `info`

1. **Użyj polecenia `man man` i zapoznaj się ze strukturą stron podręcznika (`man pages`).**  
   Strony `man` mają ustandaryzowaną strukturę:  
   - **NAME** – nazwa polecenia i krótki opis.  
   - **SYNOPSIS** – składnia użycia polecenia.  
   - **DESCRIPTION** – szczegółowy opis działania.  
   - **OPTIONS** – dostępne przełączniki (opcje).  
   - **EXAMPLES** – przykłady użycia (nie zawsze występują).  
   - **SEE ALSO** – odnośniki do powiązanych poleceń.

2. **Przejrzyj stronę podręcznika dla polecenia `ls`.**  
   - Polecenie `ls` należy do **sekcji 1** (`man 1 ls`), czyli poleceń użytkownika.  
   - Przykładowe opcje sortowania wyników:  
     - `-t` – sortuj według czasu modyfikacji.  
     - `-S` – sortuj według rozmiaru.  
     - `--sort=extension` – sortuj według rozszerzenia plików.  
   - Przydatne przełączniki:  
     - `-l` – widok długi (lista).  
     - `-a` – pokaż pliki ukryte.  
     - `-h` – rozmiary w formacie czytelnym dla człowieka.

3. **Zainstaluj pakiet `info` i przejrzyj dokumentację `info` dla `pwd`.**  
   - Instalacja:  
     ```
     sudo yum install info
     ```  
   - Wyświetlenie dokumentacji:  
     ```
     info pwd
     ```  
   - Struktura `info` to drzewo dokumentacji z węzłami (nodes) i podsekcjami.  
   - Różnice względem `man`:  
     - `info` ma więcej tekstu, więcej kontekstu i odnośników.  
     - Nawigacja klawiszowa (np. `n` – next, `p` – previous, `u` – up, `q` – quit).  
     - Pozwala przeglądać dokumentację jako książkę, nie tylko pojedynczą stronę.

4. **Zainstaluj pakiet `mc` i sprawdź dokumentację `man` i `info`.**  
   - Instalacja:  
     ```
     sudo yum install mc
     ```  
   - Sprawdzenie dokumentacji:  
     ```
     man mc
     info mc
     ```  
   - `man mc` – dostępna, zawiera dokładny opis skrótów klawiszowych i funkcji.  
   - `info mc` – może nie być dostępna; niektóre pakiety nie dostarczają dokumentacji `info`.  
   - Wbudowana pomoc w `mc`:  
     - Uruchom `mc`, naciśnij klawisz **F1**.  
     - Wyświetla się kontekstowa pomoc w formie tekstowej wewnątrz programu.

