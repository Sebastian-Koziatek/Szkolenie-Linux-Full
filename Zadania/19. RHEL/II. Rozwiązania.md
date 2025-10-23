# Rozwiązania - RHEL

## 1. Daj swojemu użytkownikowi "szkolenie" uprawnienia do używania polecenia sudo

```
Metoda 1 - Dodanie do grupy wheel:
sudo usermod -aG wheel szkolenie

Wyjaśnienie:
- usermod = modyfikuj użytkownika
- -aG = append to Group (dodaj do grupy)
- wheel = grupa z uprawnieniami sudo w RHEL

Metoda 2 - Edycja sudoers:
sudo visudo

Dodaj linię:
szkolenie ALL=(ALL) ALL

Metoda 3 - Plik w sudoers.d:
sudo echo "szkolenie ALL=(ALL) ALL" > /etc/sudoers.d/szkolenie
sudo chmod 440 /etc/sudoers.d/szkolenie

Weryfikacja:
sudo -l -U szkolenie
groups szkolenie

Test jako użytkownik szkolenie:
su - szkolenie
sudo whoami
# Powinno pokazać 'root'

Sprawdzenie członkostwa w grupie wheel:
id szkolenie
grep wheel /etc/group
```

## 2. Zaktualizuj system, użyj menagera pakietów dnf a po aktualizacji sprawdź czy jakaś aktualizacja pozostała do wykonania.

```
Aktualizacja systemu:
sudo dnf update -y

Wyjaśnienie:
- dnf = Dandified YUM (następca YUM w RHEL 8+)
- update = aktualizuj wszystkie pakiety
- -y = automatyczne potwierdzenie (yes)

Sprawdzenie dostępnych aktualizacji po update:
dnf check-update

Alternatywnie:
dnf list updates

Sprawdzenie czy są dostępne aktualizacje bezpieczeństwa:
dnf updateinfo list security

Sprawdzenie historii aktualizacji:
dnf history

Szczegółowe informacje o ostatniej transakcji:
dnf history info

Przykład kompletnego procesu:
sudo dnf clean all          # Wyczyść cache
sudo dnf update -y          # Wykonaj aktualizację
dnf check-update           # Sprawdź czy coś zostało
echo $?                    # 0 = brak aktualizacji, 100 = są aktualizacje

Sprawdzenie rozmiaru aktualizacji przed instalacją:
dnf update --downloadonly  # Tylko pobierz
dnf update --assumeno      # Symulacja bez wykonania
```

## 3. Sprawdź jaki pakiet zawiera program który pozwoli Ci sprawdzić czy musisz wykonać restart systemu po aktualizacji i zainstaluj go

```
Wyszukiwanie pakietu zawierającego needs-restarting:
dnf provides needs-restarting
dnf provides */needs-restarting

Wynik powinien pokazać:
yum-utils-4.x.x-x.el8.noarch : Utilities based upon the yum package manager

Instalacja pakietu:
sudo dnf install yum-utils

Alternatywne wyszukiwanie:
dnf search needs-restarting
dnf search restart

Weryfikacja instalacji:
which needs-restarting
needs-restarting --help

Sprawdzenie zawartości pakietu yum-utils:
rpm -ql yum-utils | grep needs
dnf repoquery --list yum-utils

Inne przydatne narzędzia w yum-utils:
- debuginfo-install
- find-repos-of-install
- package-cleanup
- repo-graph
- repoclosure
- repoquery
- reposync
- yum-builddep
- yum-config-manager
- yum-debug-dump
- yumdownloader
```

## 4. Sprawdź czy musisz wykonać restart systemu

```
Podstawowe sprawdzenie z needs-restarting:
needs-restarting

Sprawdzenie czy kernel wymaga restartu:
needs-restarting -r

Sprawdzenie które usługi wymagają restartu:
needs-restarting -s

Wszystkie opcje jednocześnie:
needs-restarting -r -s

Wyjaśnienie kodów wyjścia:
echo $?
# 0 = nie trzeba restartować
# 1 = restart wymagany

Sprawdzenie aktualnego kernela vs zainstalowanego:
uname -r                           # Aktualny kernel
rpm -q kernel --last              # Ostatnio zainstalowane kernele

Sprawdzenie czy są nowe kernele:
dnf list installed kernel
dnf list available kernel

Alternatywne metody sprawdzenia:
# Sprawdzenie czy plik /var/run/reboot-required istnieje (Ubuntu/Debian)
ls -la /var/run/reboot-required 2>/dev/null

# Sprawdzenie uptime vs czasu instalacji ostatnich pakietów
uptime
rpm -qa --last | head -5

# Sprawdzenie czy systemd wymaga restartu
systemctl is-system-running
```

## 5. Zainstaluj pakiet mc

```
Instalacja Midnight Commander:
sudo dnf install mc

Weryfikacja instalacji:
which mc
mc --version
rpm -qi mc

Sprawdzenie czy mc jest dostępny:
dnf list available mc
dnf info mc

Instalacja z dodatkowymi informacjami:
sudo dnf install -v mc

Sprawdzenie zależności przed instalacją:
dnf deplist mc

Test uruchomienia:
mc --help
mc -V

Sprawdzenie plików zainstalowanych przez mc:
rpm -ql mc

Sprawdzenie rozmiaru pakietu:
dnf info mc | grep Size
rpm -qi mc | grep Size

Lokalizacja plików konfiguracyjnych mc:
find /etc -name "*mc*" 2>/dev/null
ls -la ~/.config/mc/ 2>/dev/null
```

## 6. Sprawdź komendą man opis programu mc

```
Otwarcie strony podręcznika mc:
man mc

Przydatne skróty w man:
- Spacja: następna strona
- b: poprzednia strona
- /tekst: wyszukiwanie
- n: następne wystąpienie
- q: wyjście
- h: pomoc

Sprawdzenie czy strona man istnieje:
man -w mc
whatis mc

Sprawdzenie wszystkich sekcji man dla mc:
man -a mc
apropos mc

Wyświetlenie konkretnej sekcji:
man 1 mc

Eksport strony man do pliku tekstowego:
man mc > mc_manual.txt
man mc | col -b > mc_manual_clean.txt

Sprawdzenie lokalizacji pliku man:
man -w mc
find /usr/share/man -name "*mc*"

Alternatywne formaty dokumentacji:
info mc
mc --help
dnf info mc
```

## 7. Sprawdź stronę pomocy za pomocą polecenia man dla pakietu mc

```
Główna strona podręcznika:
man mc

Sekcje w man mc:
- NAME: Nazwa i krótki opis
- SYNOPSIS: Składnia polecenia
- DESCRIPTION: Szczegółowy opis
- OPTIONS: Opcje wiersza poleceń
- FILES: Pliki konfiguracyjne
- SEE ALSO: Powiązane polecenia

Kluczowe informacje z man mc:

Opcje wiersza poleceń:
-a: wyłącz użycie znaków graficznych
-c: kolorowy tryb
-d: wyłącz mysz
-e: edytuj plik
-f: wyświetl ścieżkę startową
-v: wyświetl plik

Pliki konfiguracyjne (z man):
~/.config/mc/ini - główny plik konfiguracyjny
~/.config/mc/hotlist - ulubione katalogi
~/.config/mc/panels.ini - ustawienia paneli

Powiązane polecenia (SEE ALSO):
man mcedit
man mcview
man mcdiff

Dodatkowe strony man związane z mc:
man mcedit      # Edytor mc
man mcview      # Przeglądarka mc
man mcdiff      # Porównywanie plików

Sprawdzenie wszystkich stron man zawierających mc:
apropos mc
man -k mc
```

## 8. Sprawdź jakie serwisy są uruchomione w systemie

```
Wszystkie aktywne serwisy:
systemctl list-units --type=service --state=active

Tylko uruchomione serwisy:
systemctl list-units --type=service --state=running

Wszystkie serwisy (aktywne i nieaktywne):
systemctl list-units --type=service --all

Krótka lista tylko nazw:
systemctl list-units --type=service --state=active --no-legend --no-pager | awk '{print $1}'

Serwisy z niepowodzeniami:
systemctl list-units --type=service --state=failed

Sprawdzenie konkretnego serwisu:
systemctl status httpd
systemctl is-active httpd
systemctl is-enabled httpd

Serwisy włączone do autostartu:
systemctl list-unit-files --type=service --state=enabled

Drzewo procesów systemd:
systemctl status
systemd-cgls

Statystyki systemd:
systemctl list-units --type=service | grep -c "active"
systemctl list-units --type=service | grep -c "failed"

Eksport listy serwisów:
systemctl list-units --type=service --all --no-pager > services_list.txt
```

## 9. Sprawdź status serwisu firewall oraz ssh

```
Status firewall (firewalld w RHEL):
systemctl status firewalld
systemctl is-active firewalld
systemctl is-enabled firewalld

Status SSH:
systemctl status sshd
systemctl is-active sshd
systemctl is-enabled sshd

Szczegółowe informacje:
systemctl show firewalld
systemctl show sshd

Sprawdzenie portów:
firewall-cmd --list-all            # Konfiguracja firewall
ss -tlnp | grep :22               # Port SSH
netstat -tlnp | grep :22          # Alternatywa

Logi serwisów:
journalctl -u firewalld -f        # Logi firewall w czasie rzeczywistym
journalctl -u sshd --since today  # Logi SSH z dzisiaj

Kontrola serwisów:
sudo systemctl start firewalld    # Uruchom
sudo systemctl stop firewalld     # Zatrzymaj
sudo systemctl restart firewalld  # Restart
sudo systemctl enable firewalld   # Włącz autostart
sudo systemctl disable firewalld  # Wyłącz autostart

Sprawdzenie zależności:
systemctl list-dependencies firewalld
systemctl list-dependencies sshd

Status jedną komendą:
systemctl status firewalld sshd
```

## 10. Sprawdź plik konfiguracyjny SSH i zobacz na jakim porcie działa twoja usługa SSH

```
Główny plik konfiguracyjny SSH:
sudo cat /etc/ssh/sshd_config

Znajdź port SSH:
grep -i "^port" /etc/ssh/sshd_config
grep -i "port" /etc/ssh/sshd_config | grep -v "^#"

Jeśli port nie jest zdefiniowany, domyślny to 22:
grep -E "^#.*Port|^Port" /etc/ssh/sshd_config

Sprawdzenie aktywnego portu:
ss -tlnp | grep sshd
netstat -tlnp | grep sshd
lsof -i :22

Weryfikacja konfiguracji SSH:
sudo sshd -T | grep port
sudo sshd -t                    # Test konfiguracji

Inne ważne ustawienia SSH:
grep -E "^(PermitRootLogin|PasswordAuthentication|PubkeyAuthentication)" /etc/ssh/sshd_config

Sprawdzenie czy SSH nasłuchuje:
systemctl status sshd
ps aux | grep sshd

Sprawdzenie połączeń SSH:
ss -o state established '( dport = :ssh or sport = :ssh )'
who                             # Zalogowani użytkownicy
w                               # Aktywne sesje

Backup i edycja konfiguracji:
sudo cp /etc/ssh/sshd_config /etc/ssh/sshd_config.backup
sudo nano /etc/ssh/sshd_config
sudo systemctl reload sshd     # Przeładuj po zmianach

Sprawdzenie wszystkich plików SSH:
ls -la /etc/ssh/
ls -la ~/.ssh/
```

## 11. Sprawdź do jakich subskrypcji masz dostęp w systemie RHEL

```
Sprawdzenie statusu subskrypcji:
subscription-manager status

Lista dostępnych subskrypcji:
subscription-manager list

Lista dostępnych subskrypcji w pool:
subscription-manager list --available

Aktualnie używane subskrypcje:
subscription-manager list --consumed

Informacje o systemie:
subscription-manager identity
subscription-manager version

Szczegółowe informacje o subskrypcji:
subscription-manager list --available --all
subscription-manager list --consumed --all

Sprawdzenie repozytoriów:
subscription-manager repos --list
subscription-manager repos --list-enabled

Informacje o produkcie:
subscription-manager list --installed

Sprawdzenie połączenia z Red Hat:
subscription-manager refresh

Status rejestracji:
subscription-manager identity

Sprawdzenie faktów o systemie:
subscription-manager facts

Eksport informacji o subskrypcji:
subscription-manager list --consumed > subscription_info.txt

Sprawdzenie czy system jest zarejestrowany:
subscription-manager status | grep "System Purpose"

Jeśli system nie jest zarejestrowany:
sudo subscription-manager register --username=your_username

Dostęp do Customer Portal:
# Możesz też sprawdzić na: https://access.redhat.com/management/subscriptions

Sprawdzenie limitów subskrypcji:
subscription-manager list --available | grep -A 10 -B 5 "Pool ID"
```

## Dodatkowe przydatne komendy RHEL

```
Informacje o wersji RHEL:
cat /etc/redhat-release
cat /etc/os-release
hostnamectl

Sprawdzenie repozytorium:
dnf repolist
dnf repolist all

Konfiguracja sieci:
nmcli con show
ip addr show
nmtui

Zarządzanie użytkownikami:
id
groups
getent passwd
getent group

Sprawdzenie zasobów systemu:
free -h
df -h
lscpu
lsblk

Konfiguracja czasu:
timedatectl
chrony sources

SELinux:
getenforce
sestatus
semanage port -l | grep ssh

Logi systemowe:
journalctl --since today
journalctl -u sshd
journalctl -f

Aktualizacje bezpieczeństwa:
dnf updateinfo list security
dnf update --security
```