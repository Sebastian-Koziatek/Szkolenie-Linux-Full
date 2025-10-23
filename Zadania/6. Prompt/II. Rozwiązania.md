# Rozwiązania - Prompt

## 1. Wygeneruj swój własny styl wiersza poleceń dla powłoki bash.

```
Generatory prompt dla bash:

Popularne strony do generowania:
- https://scriptim.github.io/bash-prompt-generator/
- https://bashrcgenerator.com/
- https://ezprompt.net/

Proces tworzenia custom prompt:

1. Wybierz elementy prompt:
   - Nazwa użytkownika (\u)
   - Nazwa hosta (\h)
   - Bieżący katalog (\w lub \W)
   - Czas (\t, \T, \@)
   - Data (\d)
   - Numer polecenia (\#)

2. Wybierz kolory:
   - \[\033[31m\] - czerwony
   - \[\033[32m\] - zielony
   - \[\033[33m\] - żółty
   - \[\033[34m\] - niebieski
   - \[\033[35m\] - magenta
   - \[\033[36m\] - cyan
   - \[\033[0m\]  - reset koloru

3. Przykładowe custom prompt:

Podstawowy kolorowy prompt:
export PS1="\[\033[32m\]\u@\h\[\033[0m\]:\[\033[34m\]\w\[\033[0m\]\$ "

Zaawansowany prompt z czasem:
export PS1="\[\033[36m\][\t]\[\033[0m\] \[\033[32m\]\u@\h\[\033[0m\]:\[\033[34m\]\w\[\033[0m\]\$ "

Prompt z git branch (wymaga git):
parse_git_branch() {
    git branch 2> /dev/null | sed -e '/^[^*]/d' -e 's/* \(.*\)/(\1)/'
}
export PS1="\[\033[32m\]\u@\h\[\033[0m\]:\[\033[34m\]\w\[\033[33m\]\$(parse_git_branch)\[\033[0m\]\$ "

Wieloliniowy prompt:
export PS1="\[\033[36m\]┌─[\[\033[32m\]\u@\h\[\033[36m\]]─[\[\033[34m\]\w\[\033[36m\]]\n└─\[\033[0m\]\$ "

Prompt z statusem ostatniego polecenia:
export PS1='\[\033[32m\]\u@\h\[\033[0m\]:\[\033[34m\]\w\[\033[0m\]$(if [ $? -eq 0 ]; then echo "\[\033[32m\] ✓"; else echo "\[\033[31m\] ✗"; fi)\[\033[0m\]\$ '

Zmienne używane w prompt:
\u - nazwa użytkownika
\h - nazwa hosta (krótka)
\H - pełna nazwa hosta
\w - pełna ścieżka do katalogu roboczego
\W - nazwa bieżącego katalogu
\d - data w formacie "Wkd Mon Date"
\t - czas w formacie 24-godzinnym HH:MM:SS
\T - czas w formacie 12-godzinnym HH:MM:SS
\@ - czas w formacie 12-godzinnym z AM/PM
\# - numer polecenia w historii
\! - numer polecenia w historii
\$ - wyświetla $ dla zwykłego użytkownika, # dla root
```

## 2. Zapisz wygenerowany bash w pliku konfiguracyjnym .bashrc.

```
Kroki edycji .bashrc:

1. Przejdź do katalogu domowego:
cd ~

2. Otwórz .bashrc w edytorze:
nano .bashrc

3. Znajdź sekcję PS1 lub dodaj na końcu pliku:
# Custom prompt
export PS1="twój_wygenerowany_prompt"

Przykład dodania do .bashrc:

# Backup oryginalnego prompt
# export PS1='\u@\h:\w\$ '

# Custom colorful prompt
export PS1="\[\033[32m\]\u@\h\[\033[0m\]:\[\033[34m\]\w\[\033[0m\]\$ "

Alternatywne metody:

Dodaj za pomocą echo:
echo 'export PS1="\[\033[32m\]\u@\h\[\033[0m\]:\[\033[34m\]\w\[\033[0m\]\$ "' >> ~/.bashrc

Edytuj z vim:
vim ~/.bashrc

Sprawdź zawartość .bashrc:
cat ~/.bashrc | grep PS1

Backup .bashrc przed zmianami:
cp ~/.bashrc ~/.bashrc.backup

Lokalizacje plików konfiguracyjnych bash:
~/.bashrc - dla non-login shells
~/.bash_profile - dla login shells
~/.profile - uniwersalny dla różnych shell'i
/etc/bash.bashrc - systemowy bashrc

Debugowanie .bashrc:
bash -x ~/.bashrc  # Uruchom z debugowaniem

Sprawdź składnię:
bash -n ~/.bashrc  # Sprawdź składnię bez wykonywania
```

## 3. Załaduj ponownie powłokę.

```
Różne sposoby przeładowania konfiguracji:

1. Source .bashrc:
source ~/.bashrc

2. Dot command (identyczny z source):
. ~/.bashrc

3. Nowa instancja bash:
bash

4. Exec bash (zastąpi obecną sesję):
exec bash

5. Logout i login ponownie:
exit
# Zaloguj się ponownie

6. Dla nowych terminali:
# Otwórz nowy terminal - automatycznie załaduje .bashrc

Weryfikacja czy prompt się zmienił:
- Prompt powinien wyglądać zgodnie z konfiguracją
- Sprawdź czy kolory działają
- Sprawdź czy wszystkie elementy są wyświetlane

Debugowanie problemów:

Sprawdź czy .bashrc jest ładowany:
echo "Bashrc loaded" >> ~/.bashrc
source ~/.bashrc

Sprawdź zmienną PS1:
echo $PS1

Tymczasowe testowanie prompt:
PS1="test prompt\$ "  # Zmieni tylko dla bieżącej sesji

Powrót do oryginalnego prompt:
unset PS1  # Użyje domyślnego
source ~/.bashrc  # Lub przeładuj konfigurację

Sprawdź która powłoka jest używana:
echo $SHELL
ps -p $$

Sprawdź czy to login shell:
echo $0
# Jeśli zaczyna się od '-', to login shell

Różnice między typami shell:
- Login shell: ładuje ~/.bash_profile, ~/.profile
- Non-login shell: ładuje ~/.bashrc
- Interactive vs non-interactive

Dodatkowe konfiguracje prompt:

PROMPT_COMMAND - wykonywane przed każdym prompt:
export PROMPT_COMMAND='echo "Czas: $(date)"'

PS2 - prompt dla wieloliniowych poleceń:
export PS2="> "

PS3 - prompt dla select:
export PS3="Wybierz opcję: "

PS4 - prompt dla debug mode:
export PS4="+ "

Przydatne funkcje w prompt:

# Funkcja pokazująca git branch
parse_git_branch() {
    git branch 2> /dev/null | sed -e '/^[^*]/d' -e 's/* \(.*\)/(\1)/'
}

# Funkcja pokazująca load average
load_avg() {
    uptime | awk '{print $10 $11 $12}'
}

# Prompt z funkcjami
export PS1="\u@\h:\w\$(parse_git_branch) \$ "
```