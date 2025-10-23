# Rozwiązania - Root, sudo, su

## 1. Czym się różni konto root od konta użytkownika?

```
Konto root (superuser):

Uprawnienia:
- UID = 0 (User ID zero)
- Pełny dostęp do wszystkich plików i katalogów
- Może modyfikować dowolne pliki systemowe
- Może instalować/usuwać oprogramowanie
- Może zarządzać usługami systemowymi
- Może tworzyć/usuwać konta użytkowników
- Może montować/odmontowywać systemy plików

Możliwości:
- Obejście kontroli dostępu (permissions)
- Dostęp do wszystkich urządzeń (/dev)
- Modyfikacja jądra systemu
- Zarządzanie siecią i firewall
- Dostęp do wszystkich procesów

Katalog domowy: /root
Shell: zwykle /bin/bash
Prompt: # (hash/kratka)

Konto użytkownika:

Uprawnienia:
- UID > 0 (zwykle 1000+)
- Dostęp tylko do własnych plików
- Ograniczony dostęp do plików systemowych
- Nie może instalować oprogramowania systemowego
- Nie może modyfikować konfiguracji systemowej

Ograniczenia:
- Kontrola dostępu przez uprawnienia plików
- Brak dostępu do /etc, /boot, /root
- Nie może zabijać procesów innych użytkowników
- Nie może montować systemów plików

Katalog domowy: /home/username
Prompt: $ (dolar)

Bezpieczeństwo:
- Root: maksymalne ryzyko - jeden błąd może zniszczyć system
- User: ograniczone ryzyko - może uszkodzić tylko własne dane

Filozofia Linux:
- Principle of least privilege
- Używaj root tylko gdy niezbędne
- Codzienne zadania jako zwykły użytkownik
```

## 2. Czym jest sudo?

```
sudo (substitute user do / superuser do):

Definicja:
- Mechanizm delegacji uprawnień administratora
- Pozwala zwykłym użytkownikom wykonywać polecenia z uprawnieniami root
- Tymczasowe podniesienie uprawnień
- Kontrolowany dostęp do funkcji administratora

Główne cechy:

Bezpieczeństwo:
- Wymaga hasła użytkownika (nie root)
- Logowanie wszystkich działań
- Granularna kontrola uprawnień
- Timeout sesji (domyślnie 15 minut)

Konfiguracja:
- Plik /etc/sudoers
- Grupy użytkowników (wheel, sudo, admin)
- Reguły per-user i per-command
- Aliasy poleceń i użytkowników

Podstawowe użycie:
sudo polecenie                    # Wykonaj polecenie jako root
sudo -u username polecenie        # Wykonaj jako inny użytkownik
sudo -i                          # Interactive shell jako root
sudo -s                          # Shell jako root
sudo -l                          # Lista dostępnych poleceń

Zalety sudo:
- Auditowanie (logi w /var/log/auth.log)
- Brak potrzeby dzielenia hasła root
- Granularne uprawnienia
- Łatwiejsze zarządzanie dostępem
- Możliwość odwołania uprawnień

Logi sudo:
tail /var/log/auth.log | grep sudo
journalctl | grep sudo

Przykłady użycia:
sudo apt update                   # Aktualizacja pakietów
sudo systemctl restart apache2   # Restart usługi
sudo mount /dev/sdb1 /mnt        # Montowanie dysku
sudo useradd newuser             # Dodanie użytkownika

Konfiguracja sudoers:
visudo                           # Bezpieczna edycja /etc/sudoers
```

## 3. Jak z poziomu użytkownika zalogować się do konta root?

```
Metody logowania do root:

1. su (substitute user):
su -
# Wymaga hasła root
# - oznacza login shell (pełne środowisko root)

su
# Zmienia na root ale zachowuje środowisko użytkownika

2. sudo su:
sudo su -
# Używa hasła użytkownika (jeśli ma uprawnienia sudo)
# Bezpieczniejsze od dzielenia hasła root

3. sudo -i:
sudo -i
# Interactive login shell jako root
# Preferowany sposób

4. Bezpośrednie logowanie:
login root
# Na konsoli systemowej
# Wymaga hasła root

5. SSH (jeśli włączone):
ssh root@localhost
# Wymaga konfiguracji SSH dla root

Porównanie metod:

su -:
- Wymaga hasła root
- Pełne środowisko root
- Tradycyjna metoda

sudo su -:
- Wymaga hasła użytkownika
- Logowane przez sudo
- Bezpieczniejsze

sudo -i:
- Wymaga hasła użytkownika  
- Preferowane przez sudo
- Najlepsze practices

Weryfikacja tożsamości root:
whoami                    # Powinno pokazać 'root'
id                       # UID=0
echo $HOME               # /root
pwd                      # Lokalizacja

Wyjście z root:
exit
logout
Ctrl+D

Uwagi bezpieczeństwa:
- Używaj sudo zamiast su gdy możliwe
- Nigdy nie włączaj SSH dla root w produkcji
- Ogranicz czas przebywania jako root
- Używaj sudo -i zamiast sudo su -
```

## 4. Zaloguj się do konta root i korzystając z pakietu sudo dopisz konto swojego użytkownika do listy kont uprawnionych.

```
Kroki dodania użytkownika do sudo:

1. Zaloguj się jako root:
sudo -i
# lub: su -

2. Sprawdź istniejącą konfigurację:
cat /etc/sudoers | grep -E "^%|^[a-zA-Z]"

3. Metoda 1 - Dodanie do grupy wheel/sudo:

RHEL/CentOS/Fedora:
usermod -aG wheel username

Debian/Ubuntu:
usermod -aG sudo username

4. Metoda 2 - Edycja /etc/sudoers:
visudo

Dodaj linię:
username ALL=(ALL) ALL

5. Metoda 3 - Utworzenie pliku w sudoers.d:
echo "username ALL=(ALL) ALL" > /etc/sudoers.d/username
chmod 440 /etc/sudoers.d/username

Weryfikacja:
1. Wyjdź z root:
exit

2. Testuj sudo:
sudo whoami
# Powinno pokazać 'root'

3. Sprawdź uprawnienia:
sudo -l

Przykłady konfiguracji w sudoers:

Pełne uprawnienia:
username ALL=(ALL) ALL

Bez hasła:
username ALL=(ALL) NOPASSWD: ALL

Tylko konkretne polecenia:
username ALL=(ALL) /usr/bin/systemctl, /usr/bin/mount

Grupa z pełnymi uprawnieniami:
%wheel ALL=(ALL) ALL

Sprawdzenie członkostwa w grupach:
groups username
id username

Testowanie różnych poleceń sudo:
sudo ls /root
sudo systemctl status sshd
sudo cat /etc/shadow

Dodatkowe opcje sudoers:

Aliasy użytkowników:
User_Alias ADMINS = john, jane, bob
ADMINS ALL=(ALL) ALL

Aliasy hostów:
Host_Alias SERVERS = server1, server2
username SERVERS=(ALL) ALL

Aliasy poleceń:
Cmnd_Alias SERVICES = /usr/bin/systemctl
username ALL=(ALL) SERVICES

Domyślne ustawienia:
Defaults secure_path="/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin"
Defaults timestamp_timeout=15
Defaults !visiblepw
```

## 5. Czym się różni sudo su - od su?

```
Różnice między 'sudo su -' a 'su':

sudo su -:

Mechanizm uwierzytelnienia:
- Wymaga hasła UŻYTKOWNIKA
- Sprawdza uprawnienia sudo użytkownika
- Loguje działanie w systemie audytu

Bezpieczeństwo:
- Nie wymaga znajomości hasła root
- Wszystkie działania są logowane
- Można ograniczyć kto może używać
- Timeout automatyczny

Audyt:
- Zapisuje w /var/log/auth.log
- Możliwość śledzenia kto i kiedy
- Integracja z systemami monitorowania

Konfiguracja:
- Kontrolowane przez /etc/sudoers
- Granularne uprawnienia
- Możliwość ograniczenia poleceń

su:

Mechanizm uwierzytelnienia:
- Wymaga hasła ROOT
- Bezpośredni dostęp do konta root
- Brak dodatkowego logowania

Bezpieczeństwo:
- Wymaga dzielenia hasła root
- Trudniejsze audytowanie
- Każdy kto zna hasło może się zalogować

Audyt:
- Minimalne logowanie
- Trudno śledzić działania
- Brak granularnej kontroli

Porównanie praktyczne:

sudo su -:
$ sudo su -
[sudo] password for user: <hasło_użytkownika>
# whoami
root

su:
$ su -
Password: <hasło_root>
# whoami  
root

Inne warianty:

sudo -i:
- Preferowany sposób
- Login shell jako root
- Pełne środowisko root
- Logowanie przez sudo

sudo -s:
- Shell jako root
- Zachowuje obecne środowisko
- Nie zmienia $HOME

sudo su:
- Bez -, nie zmienia środowiska
- Non-login shell
- Może nie załadować profilu root

Środowisko po zalogowaniu:

su -:
- $HOME = /root
- PATH = root's PATH
- Pełny profil root

sudo su -:
- $HOME = /root  
- PATH = root's PATH
- Pełny profil root
- + logowanie sudo

su (bez -):
- $HOME = user's home
- PATH = user's PATH
- Środowisko użytkownika

Best practices:
1. Używaj sudo -i zamiast sudo su -
2. Unikaj zwykłego su
3. Nigdy nie udostępniaj hasła root
4. Konfiguruj sudo dla konkretnych zadań
5. Regularnie przeglądaj logi sudo

Sprawdzenie środowiska:
echo $HOME
echo $PATH
echo $USER
pwd
env | grep -E "HOME|PATH|USER"
```

## 6. Przejrzyj plik konfiguracyjny sudo i utwórz wpis który pozwoli wywoływać polecenia sudo bez hasła.

```
Przegląd pliku konfiguracyjnego sudo:

1. Bezpieczne otwieranie sudoers:
sudo visudo

Uwaga: NIGDY nie edytuj /etc/sudoers bezpośrednio!
visudo sprawdza składnię przed zapisem.

2. Struktura pliku /etc/sudoers:

Główne sekcje:
# Defaults - domyślne ustawienia
# User privilege specification - uprawnienia użytkowników
# Group privilege specification - uprawnienia grup
# Include directive - dodatkowe pliki

Przykładowa zawartość:
Defaults        env_reset
Defaults        mail_badpass
Defaults        secure_path="/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin"

root    ALL=(ALL:ALL) ALL
%admin  ALL=(ALL) ALL
%sudo   ALL=(ALL:ALL) ALL

3. Dodanie wpisu bez hasła:

Metoda 1 - Modyfikacja głównego pliku:
sudo visudo

Dodaj linię:
username ALL=(ALL) NOPASSWD: ALL

Metoda 2 - Utworzenie oddzielnego pliku:
sudo visudo -f /etc/sudoers.d/nopasswd-username

Zawartość pliku:
username ALL=(ALL) NOPASSWD: ALL

4. Różne warianty konfiguracji NOPASSWD:

Pełne uprawnienia bez hasła:
username ALL=(ALL) NOPASSWD: ALL

Tylko konkretne polecenia:
username ALL=(ALL) NOPASSWD: /usr/bin/systemctl, /usr/bin/mount

Tylko restart usług:
username ALL=(ALL) NOPASSWD: /usr/bin/systemctl restart *

Grupa bez hasła:
%wheel ALL=(ALL) NOPASSWD: ALL

Kombinacja z hasłem i bez:
username ALL=(ALL) NOPASSWD: /usr/bin/systemctl
username ALL=(ALL) /usr/bin/vi /etc/hosts

5. Testowanie konfiguracji:

Sprawdź składnię:
sudo visudo -c

Lista uprawnień:
sudo -l

Test bez hasła:
sudo whoami
# Nie powinno pytać o hasło

Test konkretnego polecenia:
sudo systemctl status sshd

6. Zaawansowane opcje:

Ograniczenie czasowe:
Defaults:username timestamp_timeout=0

Bez logów dla NOPASSWD:
Defaults:username !syslog

Wymaganie TTY:
Defaults:username requiretty

Ustawienia środowiska:
Defaults:username env_keep += "DISPLAY HOME"

7. Przykład kompletnej konfiguracji:

sudo visudo -f /etc/sudoers.d/custom-user

Zawartość:
# User privilege specification for custom-user
custom-user ALL=(ALL) NOPASSWD: ALL

# Alternative: limited commands without password
# custom-user ALL=(ALL) NOPASSWD: /usr/bin/systemctl, /usr/bin/mount, /usr/bin/umount

# Optional: specific defaults for this user
Defaults:custom-user !authenticate
Defaults:custom-user timestamp_timeout=0

8. Weryfikacja i testowanie:

Sprawdź uprawnienia:
sudo -l -U username

Test różnych poleceń:
sudo ls /root
sudo systemctl status sshd
sudo cat /etc/shadow

Sprawdź logi:
sudo tail /var/log/auth.log | grep sudo

9. Bezpieczeństwo NOPASSWD:

Zagrożenia:
- Każdy kto przejmie sesję może wykonać sudo
- Screen lock nie chroni przed sudo
- Skrypty mogą automatycznie używać sudo

Mitygacja:
- Ogranicz NOPASSWD do konkretnych poleceń
- Używaj timestamp_timeout=0
- Regularnie przeglądaj logi
- Rozważ 2FA dla krytycznych systemów

10. Usuwanie konfiguracji NOPASSWD:

Usuń wpis z sudoers:
sudo visudo

Usuń plik w sudoers.d:
sudo rm /etc/sudoers.d/nopasswd-username

Sprawdź czy zmiany zadziałały:
sudo -l
sudo whoami  # Powinno pytać o hasło
```