
1. **Utwórz alias tymczasowy do wyświetlenia aktualnej daty i godziny:**
   
   ```bash
   alias now='date'
   ```

2. **Utwórz alias tymczasowy do wyświetlenia listy plików w katalogu `/etc`:**
   
   ```bash
   alias etc='ls /etc'
   ```

3. **Utwórz alias tymczasowy do wyświetlenia listy zainstalowanych pakietów:**
   
   ```bash
   alias packages='yum list installed'
   ```

4. **Utwórz alias tymczasowy do szybkiego przejścia do katalogu domowego:**
   
   ```bash
   alias home='cd ~'
   ```

5. **Utwórz alias tymczasowy do wyświetlenia zajętości dysku w formie graficznej:**
   
   ```bash
   alias disk='df -h'
   ```

6. **Utwórz stały alias do aktualizacji systemu, wyczyszczenia cache, metadanych i nagłówków menedżera pakietów oraz wyświetlenia informacji o sukcesie:**
   
```bash
alias update="sudo yum update; sudo clean all; clear; echo 'Aktualizacja udana'"
```