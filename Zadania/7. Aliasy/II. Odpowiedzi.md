# Dzień 6 – Odpowiedzi: Aliasowanie poleceń

1. **Utwórz tymczasowy alias `czas` do wyświetlenia aktualnej daty i godziny.**  
   ```bash
   alias czas="date"
   ```

2. **Utwórz tymczasowy alias `etc` do szybkiego wyświetlenia zawartości katalogu `/etc`.**  
   ```bash
   alias etc="ls -la /etc"
   ```

3. **Utwórz tymczasowy alias `pakiety` do wyświetlenia listy wszystkich zainstalowanych pakietów.**  
   - Dla systemów opartych o YUM/DNF (RHEL, CentOS, Fedora):  
     ```bash
     alias pakiety="dnf list installed"
     ```
   - Lub:  
     ```bash
     alias pakiety="yum list installed"
     ```

4. **Utwórz tymczasowy alias `dom` do szybkiego przejścia do katalogu domowego.**  
   ```bash
   alias dom="cd ~"
   ```

5. **Utwórz tymczasowy alias `dysk` do wyświetlenia zajętości dysku w formie czytelnej dla użytkownika.**  
   ```bash
   alias dysk="df -h"
   ```

6. **Utwórz stały alias `aktualizuj` do wykonania aktualizacji systemu, wyczyszczenia cache oraz wyświetlenia komunikatu o powodzeniu.**  
   - Dodaj do pliku `~/.bashrc` lub `~/.bash_aliases`:  
     ```bash
     alias aktualizuj="sudo dnf update -y && sudo dnf clean all && echo 'Aktualizacja zakończona pomyślnie!'"
     ```
   - Użytkownicy systemów z `yum`:  
     ```bash
     alias aktualizuj="sudo yum update -y && sudo yum clean all && echo 'Aktualizacja zakończona pomyślnie!'"
     ```
   - Po zapisaniu pliku wykonaj:  
     ```bash
     source ~/.bashrc
     ```

