# Rozwiązania - Crontab

## 1. Korzystając z generatora czasu do crona, stwórz wpis który co minutę będzie wysłał wiadomość do wszystkich użytkowników systemu z informacją "Crontab pozdrawia".

```
Edycja crontab dla użytkownika root:
sudo crontab -e

Wpis do dodania:
* * * * * wall "Crontab pozdrawia"

Wyjaśnienie formatu cron:
* * * * * polecenie
│ │ │ │ │
│ │ │ │ └─── dzień tygodnia (0-7, gdzie 0 i 7 = niedziela)
│ │ │ └───── miesiąc (1-12)
│ │ └─────── dzień miesiąca (1-31)
│ └───────── godzina (0-23)
└─────────── minuta (0-59)

Alternatywne polecenia do wysyłania wiadomości:
* * * * * echo "Crontab pozdrawia" | wall
* * * * * /usr/bin/wall "Crontab pozdrawia"

Dodanie do crontab systemowego:
sudo echo "* * * * * root wall 'Crontab pozdrawia'" >> /etc/crontab

Sprawdzenie składni w generatorach online:
# Popularne generatory cron:
# - https://crontab.guru/
# - https://crontab-generator.org/
# - https://cron-job.org/en/

Weryfikacja wpisu:
sudo crontab -l

Przykładowe inne interwały:
*/5 * * * * polecenie     # Co 5 minut
0 * * * * polecenie       # Co godzinę (o pełnej godzinie)
0 0 * * * polecenie       # Codziennie o północy
0 0 * * 1 polecenie       # Każdy poniedziałek o północy

Test polecenia wall:
wall "Test wiadomości"
echo "Test" | wall

Sprawdzenie czy użytkownicy otrzymują wiadomości:
# Zaloguj się jako różni użytkownicy w osobnych terminalach
# Wiadomość powinna pojawić się na wszystkich konsolach
```

## 2. Zrestartuj serwis crona aby załadować nowe ustawienia.

```
Restart serwisu cron:
sudo systemctl restart crond           # RHEL/CentOS/Fedora
sudo systemctl restart cron            # Debian/Ubuntu

Sprawdzenie statusu serwisu:
systemctl status crond                 # RHEL/CentOS/Fedora
systemctl status cron                  # Debian/Ubuntu

Przeładowanie konfiguracji (alternatywa do restart):
sudo systemctl reload crond
sudo systemctl reload cron

Sprawdzenie czy serwis jest uruchomiony:
systemctl is-active crond
systemctl is-active cron

Sprawdzenie czy serwis jest włączony na stałe:
systemctl is-enabled crond
systemctl is-enabled cron

Włączenie autostartu serwisu (jeśli nie jest włączony):
sudo systemctl enable crond
sudo systemctl enable cron

Sprawdzenie procesów cron:
ps aux | grep cron
pgrep cron

Logi serwisu cron:
journalctl -u crond -f               # Follow logs RHEL/CentOS
journalctl -u cron -f                # Follow logs Debian/Ubuntu

Sprawdzenie logów w tradycyjnych plikach:
tail -f /var/log/cron                # RHEL/CentOS
tail -f /var/log/syslog | grep cron  # Debian/Ubuntu

Restart z weryfikacją:
sudo systemctl restart crond && systemctl status crond
sudo systemctl restart cron && systemctl status cron

Sprawdzenie czy restart był konieczny:
# W nowoczesnych systemach cron automatycznie wykrywa zmiany
# Restart nie zawsze jest konieczny, ale jest dobrą praktyką
```

## 3. Wyświetl wszystkie zaplanowane procesy crona.

```
Sprawdzenie crontab bieżącego użytkownika:
crontab -l

Sprawdzenie crontab innego użytkownika (jako root):
sudo crontab -u username -l

Sprawdzenie crontab wszystkich użytkowników:
sudo crontab -u root -l
for user in $(cut -f1 -d: /etc/passwd); do
    echo "=== $user ==="
    sudo crontab -u $user -l 2>/dev/null
done

Sprawdzenie systemowego crontab:
cat /etc/crontab

Sprawdzenie katalogów cron:
ls -la /etc/cron.d/
ls -la /etc/cron.hourly/
ls -la /etc/cron.daily/
ls -la /etc/cron.weekly/
ls -la /etc/cron.monthly/

Zawartość katalogów systemowych:
cat /etc/cron.d/*
ls -la /etc/cron.daily/
ls -la /etc/cron.weekly/
ls -la /etc/cron.monthly/

Sprawdzenie uprawnień plików cron:
ls -la /var/spool/cron/         # RHEL/CentOS
ls -la /var/spool/cron/crontabs/ # Debian/Ubuntu

Aktywne zadania cron (przez logi):
grep CRON /var/log/cron | tail -10        # RHEL/CentOS
grep cron /var/log/syslog | tail -10      # Debian/Ubuntu

Sprawdzenie ostatnich wykonań:
journalctl -u crond --since "1 hour ago"
journalctl -u cron --since "1 hour ago"

Lista wszystkich plików związanych z cron:
find /etc -name "*cron*" -type f
find /var/spool -name "*cron*" -type d

Sprawdzenie anacron (dla zadań w przypadku wyłączonego systemu):
cat /etc/anacrontab
ls -la /var/spool/anacron/

Sprawdzenie at jobs (jednorazowe zadania):
atq                             # Lista zaplanowanych zadań at
at -l                          # Alternative
```

## 4. Sprawdź listę zaplanowanych zadań cron dla użytkownika szkolenie

```
Sprawdzenie crontab użytkownika szkolenie:
sudo crontab -u szkolenie -l

Jeśli zalogowany jako szkolenie:
crontab -l

Sprawdzenie czy użytkownik ma crontab:
sudo ls -la /var/spool/cron/szkolenie        # RHEL/CentOS
sudo ls -la /var/spool/cron/crontabs/szkolenie # Debian/Ubuntu

Sprawdzenie uprawnień dostępu do cron:
cat /etc/cron.allow 2>/dev/null | grep szkolenie
cat /etc/cron.deny 2>/dev/null | grep szkolenie

Jeśli crontab nie istnieje:
sudo crontab -u szkolenie -l
# Wynik: "no crontab for szkolenie"

Tworzenie crontab dla użytkownika szkolenie:
sudo crontab -u szkolenie -e

Przykładowy wpis dla użytkownika szkolenie:
# Backup katalogu domowego codziennie o 2:00
0 2 * * * tar -czf /tmp/backup_$(date +\%Y\%m\%d).tar.gz /home/szkolenie

Sprawdzenie logów dotyczących użytkownika szkolenie:
grep szkolenie /var/log/cron                 # RHEL/CentOS
grep szkolenie /var/log/syslog               # Debian/Ubuntu

Weryfikacja czy użytkownik może używać cron:
# Sprawdź czy szkolenie jest w allowed users
if [ -f /etc/cron.allow ]; then
    grep szkolenie /etc/cron.allow && echo "Allowed" || echo "Not in allow list"
else
    echo "No cron.allow file - checking cron.deny"
    if [ -f /etc/cron.deny ]; then
        grep szkolenie /etc/cron.deny && echo "Denied" || echo "Allowed (not in deny list)"
    else
        echo "No restrictions - all users allowed"
    fi
fi

Lista wszystkich użytkowników z crontab:
ls -la /var/spool/cron/
ls -la /var/spool/cron/crontabs/

Sprawdzenie przez sudo:
sudo -u szkolenie crontab -l

Historia wykonań zadań użytkownika szkolenie:
grep "szkolenie" /var/log/cron | tail -10
journalctl | grep szkolenie | grep CRON
```

## 5. Jakimi znakami rozdzielisz poszczególne polecenia które możesz zawrzeć w cronie?

```
Znaki rozdzielające polecenia w cron:

1. Średnik (;) - sekwencyjne wykonanie:
* * * * * polecenie1; polecenie2; polecenie3

2. Ampersand (&) - równoległe wykonanie:
* * * * * polecenie1 & polecenie2 & polecenie3

3. Podwójny ampersand (&&) - warunkowe wykonanie (jeśli poprzednie się udało):
* * * * * polecenie1 && polecenie2 && polecenie3

4. Podwójna kreska (||) - wykonanie jeśli poprzednie się nie udało:
* * * * * polecenie1 || polecenie2

5. Pipe (|) - przekazanie wyjścia jednego polecenia do drugiego:
* * * * * ps aux | grep apache | wc -l

Przykłady praktyczne:

Sekwencyjne wykonanie (;):
* * * * * cd /home/user; ls -la; date

Warunkowe wykonanie (&&):
* * * * * ping -c 1 google.com && echo "Internet działa" | mail admin@domain.com

Wykonanie jeśli pierwsze nie udało się (||):
* * * * * systemctl is-active httpd || systemctl start httpd

Kombinacje:
* * * * * cd /backup && tar -czf backup.tar.gz /home/user && echo "Backup OK" || echo "Backup FAILED"

Pipe do przetwarzania:
* * * * * ps aux | grep apache | wc -l > /tmp/apache_count.txt

Przekierowanie wyjścia:
* * * * * polecenie > /dev/null 2>&1                    # Ukryj wszystkie wyjścia
* * * * * polecenie >> /var/log/moj_log.log 2>&1        # Dopisz do logu
* * * * * polecenie 2>&1 | logger -t CRON               # Wyślij do syslog

Grupowanie poleceń:
* * * * * (cd /backup && tar -czf backup.tar.gz /home/user)

Przykłady zaawansowane:
# Backup z walidacją
0 2 * * * cd /backup && tar -czf backup_$(date +\%Y\%m\%d).tar.gz /home/user && echo "Backup completed" | mail admin@domain.com || echo "Backup failed" | mail admin@domain.com

# Monitoring z reakcją
*/5 * * * * pgrep httpd > /dev/null || systemctl start httpd

# Czyszczenie z logowaniem
0 0 * * 0 find /tmp -type f -mtime +7 -delete && echo "$(date): Cleaned old files from /tmp" >> /var/log/cleanup.log

Uwagi o cudzysłowach:
* * * * * echo "Hello World" > /tmp/hello.txt
* * * * * echo 'Hello $USER' > /tmp/hello.txt            # Literal $USER
* * * * * echo "Hello $USER" > /tmp/hello.txt            # Expanded $USER

Escapowanie znaków specjalnych:
* * * * * echo "Current time: $(date)" > /tmp/time.txt
* * * * * echo 'Date: \$(date)' > /tmp/time.txt
```

## 6. Użyj polecenia aby usunąć utworzony wpis do crona (żeby nie zaśmiecał Ci systemu)

```
Usunięcie wpisu z crontab:

Metoda 1 - Edycja crontab:
sudo crontab -e
# Usuń linię: * * * * * wall "Crontab pozdrawia"
# Zapisz i wyjdź

Metoda 2 - Usunięcie całego crontab:
sudo crontab -r

Metoda 3 - Usunięcie crontab konkretnego użytkownika:
sudo crontab -u root -r
sudo crontab -u szkolenie -r

Bezpieczne usunięcie z backup:
sudo crontab -l > /tmp/crontab_backup.txt
sudo crontab -r

Przywrócenie z backup (gdyby było potrzebne):
sudo crontab /tmp/crontab_backup.txt

Usunięcie konkretnego wpisu przez filtrowanie:
sudo crontab -l | grep -v "wall" | sudo crontab -

Weryfikacja usunięcia:
sudo crontab -l
# Powinno pokazać "no crontab for root" lub pusty crontab

Usunięcie z systemowego crontab:
sudo nano /etc/crontab
# Usuń linię ręcznie

Usunięcie z /etc/cron.d/:
sudo rm /etc/cron.d/nazwa_pliku

Sprawdzenie czy wiadomości przestały się wyświetlać:
# Poczekaj minutę i sprawdź czy wall messages się zatrzymały

Czyszczenie logów cron (opcjonalne):
sudo truncate -s 0 /var/log/cron        # RHEL/CentOS

Sprawdzenie czy żadne zadania nie pozostały:
sudo crontab -l                         # Root crontab
crontab -l                              # Bieżący użytkownik
for user in $(cut -f1 -d: /etc/passwd); do
    echo "=== $user ==="
    sudo crontab -u $user -l 2>/dev/null || echo "No crontab"
done

Usunięcie wszystkich crontab w systemie:
for user in $(cut -f1 -d: /etc/passwd); do
    sudo crontab -u $user -r 2>/dev/null
done

Restart serwisu cron po zmianach:
sudo systemctl restart crond            # RHEL/CentOS
sudo systemctl restart cron             # Debian/Ubuntu

Monitoring czy zadania rzeczywiście się zatrzymały:
journalctl -u crond -f                  # Follow cron logs
tail -f /var/log/cron                   # Traditional logs
```

## Dodatkowe informacje o Cron

```
Formaty specjalne cron:
@reboot polecenie              # Po restarcie systemu
@yearly polecenie              # Raz w roku (0 0 1 1 *)
@annually polecenie            # To samo co @yearly
@monthly polecenie             # Raz w miesiącu (0 0 1 * *)
@weekly polecenie              # Raz w tygodniu (0 0 * * 0)
@daily polecenie               # Codziennie (0 0 * * *)
@midnight polecenie            # To samo co @daily
@hourly polecenie              # Co godzinę (0 * * * *)

Przykłady zaawansowanych wpisów:
*/15 * * * * polecenie         # Co 15 minut
0 2-4 * * * polecenie          # Codziennie o 2:00, 3:00, 4:00
0 0 1,15 * * polecenie         # 1 i 15 każdego miesiąca
0 0 * * 1-5 polecenie          # Poniedziałek-piątek
0 0 1 */3 * polecenie          # Co 3 miesiące

Zmienne środowiskowe w cron:
PATH=/usr/local/bin:/usr/bin:/bin
MAILTO=admin@domain.com
HOME=/home/user
SHELL=/bin/bash

0 2 * * * /path/to/script.sh

Debugowanie cron:
# Włącz szczegółowe logowanie
echo "cron.*    /var/log/cron.log" >> /etc/rsyslog.conf
systemctl restart rsyslog

# Test wykonania polecenia
* * * * * echo "Test: $(date)" >> /tmp/cron_test.log

Anacron dla systemów nieciągłych:
cat /etc/anacrontab

# Format anacron:
# period_in_days delay_in_minutes job-identifier command

1    5    cron.daily    run-parts /etc/cron.daily
7    25   cron.weekly   run-parts /etc/cron.weekly
@monthly 45 cron.monthly run-parts /etc/cron.monthly

Bezpieczeństwo cron:
# Kontrola dostępu
/etc/cron.allow                # Tylko ci użytkownicy mogą używać cron
/etc/cron.deny                 # Ci użytkownicy nie mogą używać cron

# Uprawnienia
ls -la /usr/bin/crontab        # Powinno mieć SUID bit
ls -la /var/spool/cron         # Właściciel: root, tylko root może czytać
```