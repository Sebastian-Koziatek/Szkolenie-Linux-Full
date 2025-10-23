# Rozwiązania - Aliasy

## 1. Utwórz tymczasowy alias `czas` do wyświetlenia aktualnej daty i godziny.

```
Polecenie:
alias czas='date'

Alternatywne wersje:
alias czas='date "+%Y-%m-%d %H:%M:%S"'
alias czas='date "+%A, %B %d, %Y - %H:%M:%S"'

Testowanie aliasu:
czas

Sprawdzenie czy alias istnieje:
alias czas
alias | grep czas

Usunięcie aliasu:
unalias czas

Wyjaśnienie:
- Alias jest aktywny tylko w bieżącej sesji
- Po zamknięciu terminala alias zostanie usunięty
- date wyświetla aktualną datę i czas systemowy
```

## 2. Utwórz tymczasowy alias `etc` do szybkiego wyświetlenia zawartości katalogu `/etc`.

```
Polecenie:
alias etc='ls -la /etc'

Alternatywne wersje:
alias etc='ls -lh /etc'              # Z czytelnym rozmiarem
alias etc='ls -la /etc | less'       # Z paginacją
alias etc='find /etc -maxdepth 1 -ls' # Z find

Testowanie:
etc

Bardziej zaawansowane wersje:
alias etc='ls -la /etc --color=auto'
alias etc='tree /etc -L 1'  # Jeśli tree jest zainstalowane

Przydatne warianty:
alias etc-conf='ls -la /etc/*.conf'
alias etc-d='ls -la /etc/*d/'
```

## 3. Utwórz tymczasowy alias `pakiety` do wyświetlenia listy wszystkich zainstalowanych pakietów.

```
Dla systemów RPM (RHEL, CentOS, Fedora):
alias pakiety='rpm -qa'
alias pakiety='yum list installed'
alias pakiety='dnf list installed'

Dla systemów DEB (Debian, Ubuntu):
alias pakiety='dpkg -l'
alias pakiety='apt list --installed'

Z sortowaniem i formatowaniem:
alias pakiety='rpm -qa | sort'
alias pakiety='rpm -qa | sort | less'

Z liczeniem pakietów:
alias pakiety='echo "Zainstalowane pakiety: $(rpm -qa | wc -l)" && rpm -qa | sort'

Testowanie:
pakiety

Warianty z filtrowaniem:
alias pakiety-kernel='rpm -qa | grep kernel'
alias pakiety-lib='rpm -qa | grep lib'
```

## 4. Utwórz tymczasowy alias `dom` do szybkiego przejścia do katalogu domowego.

```
Polecenie:
alias dom='cd ~'

Alternatywne wersje:
alias dom='cd $HOME'
alias dom='cd && pwd'    # Z wyświetleniem lokalizacji
alias dom='cd ~ && ls'   # Z listą plików

Testowanie:
dom

Sprawdzenie lokalizacji:
pwd

Przydatne warianty:
alias dom-ls='cd ~ && ls -la'
alias dom-size='cd ~ && du -sh .'
alias dom-backup='cd ~/backup'
alias dom-downloads='cd ~/Downloads'

Kombinacja z innymi poleceniami:
alias dom-clean='cd ~ && rm -f *.tmp'
```

## 5. Utwórz tymczasowy alias `dysk` do wyświetlenia zajętości dysku w formie czytelnej dla użytkownika.

```
Polecenie:
alias dysk='df -h'

Alternatywne wersje:
alias dysk='df -h | grep -v tmpfs'     # Bez systemów tymczasowych
alias dysk='df -h /'                   # Tylko root filesystem

Bardziej szczegółowe:
alias dysk='df -h && echo && du -sh ~' # Z rozmiarem katalogu domowego

Z kolorami (jeśli dostępne):
alias dysk='df -h --output=source,fstype,size,used,avail,pcent,target'

Testowanie:
dysk

Warianty specjalistyczne:
alias dysk-inode='df -i'              # Wykorzystanie i-node'ów
alias dysk-type='df -T'               # Z typami systemów plików
alias dysk-all='df -a'                # Wszystkie systemy plików

Z formatowaniem:
alias dysk='echo "=== Zajętość dysków ===" && df -h | head -1 && df -h | grep -v tmpfs | tail -n +2'
```

## 6. Utwórz stały alias `aktualizuj` do wykonania aktualizacji systemu, wyczyszczenia cache oraz wyświetlenia komunikatu o powodzeniu.

```
Dla systemów RPM (RHEL/CentOS/Fedora):

YUM:
alias aktualizuj='sudo yum update -y && sudo yum clean all && echo "System został zaktualizowany!"'

DNF:
alias aktualizuj='sudo dnf update -y && sudo dnf clean all && echo "System został zaktualizowany!"'

Dla systemów DEB (Debian/Ubuntu):
alias aktualizuj='sudo apt update && sudo apt upgrade -y && sudo apt autoremove -y && sudo apt autoclean && echo "System został zaktualizowany!"'

Zapisanie stałego aliasu w .bashrc:

1. Otwórz .bashrc:
nano ~/.bashrc

2. Dodaj na końcu pliku:
# Custom aliases
alias aktualizuj='sudo yum update -y && sudo yum clean all && echo "System został zaktualizowany!"'

3. Przeładuj konfigurację:
source ~/.bashrc

Weryfikacja stałego aliasu:
alias aktualizuj
grep aktualizuj ~/.bashrc

Testowanie:
aktualizuj

Zaawansowane wersje z logowaniem:
alias aktualizuj='sudo yum update -y && sudo yum clean all && echo "$(date): System zaktualizowany" >> ~/update.log && echo "System został zaktualizowany!"'

Z backup'em przed aktualizacją:
alias aktualizuj='sudo cp /etc/yum.conf /etc/yum.conf.backup.$(date +%Y%m%d) && sudo yum update -y && sudo yum clean all && echo "System został zaktualizowany!"'

Inne przydatne stałe aliasy do dodania w .bashrc:

# Nawigacja
alias ll='ls -la'
alias la='ls -A'
alias l='ls -CF'
alias ..='cd ..'
alias ...='cd ../..'

# Bezpieczeństwo
alias rm='rm -i'
alias cp='cp -i'
alias mv='mv -i'

# Kolory
alias ls='ls --color=auto'
alias grep='grep --color=auto'
alias fgrep='fgrep --color=auto'
alias egrep='egrep --color=auto'

# System
alias psg='ps aux | grep'
alias h='history'
alias j='jobs -l'
alias mount='mount | column -t'

# Sieć
alias ping='ping -c 5'
alias fastping='ping -c 100 -s.2'
alias ports='netstat -tulanp'

Zarządzanie aliasami:

Lista wszystkich aliasów:
alias

Sprawdzenie konkretnego aliasu:
alias nazwa_aliasu

Usunięcie aliasu (tymczasowo):
unalias nazwa_aliasu

Usunięcie wszystkich aliasów:
unalias -a

Sprawdzenie czy polecenie to alias:
type polecenie
which polecenie

Backup aliasów:
alias > ~/aliases_backup.txt

Przywrócenie aliasów:
source ~/aliases_backup.txt
```