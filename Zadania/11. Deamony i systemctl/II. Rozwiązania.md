# Rozwiązania - Deamony i systemctl

## 1. Wyświetl wszystkie serwisy w systemie i ich aktualny stan oraz lokalizację

```
Lista wszystkich serwisów z statusem:
systemctl list-units --type=service --all

Tylko aktywne serwisy:
systemctl list-units --type=service --state=active

Lista wszystkich plików unit (włącznie z lokalizacją):
systemctl list-unit-files --type=service

Szczegółowe informacje z lokalizacją:
systemctl list-unit-files --type=service | head -20

Sprawdzenie lokalizacji konkretnego serwisu:
systemctl show nginx -p FragmentPath
systemctl cat nginx

Wszystkie serwisy z pełnymi informacjami:
systemctl list-units --type=service --all --no-pager

Status konkretnego serwisu:
systemctl status nazwa_serwisu
systemctl show nazwa_serwisu

Serwisy w różnych stanach:
systemctl list-units --type=service --state=failed    # Nieudane
systemctl list-units --type=service --state=running   # Uruchomione
systemctl list-units --type=service --state=inactive  # Nieaktywne

Lokalizacje plików systemd:
/usr/lib/systemd/system/    # Domyślne pliki unit
/etc/systemd/system/        # Lokalne/custom pliki unit
/run/systemd/system/        # Tymczasowe pliki unit

Sprawdzenie ścieżek systemd:
systemd-analyze unit-paths
```

## 2. Zainstaluj silnik stron internetowych nginx i uruchom jego deamona

```
Instalacja nginx:
sudo dnf install nginx                    # RHEL/CentOS/Fedora
sudo apt install nginx                   # Debian/Ubuntu
sudo yum install nginx                   # Starsze RHEL/CentOS

Uruchomienie serwisu nginx:
sudo systemctl start nginx

Weryfikacja instalacji:
which nginx
nginx -v
rpm -qi nginx                           # RHEL/CentOS
dpkg -l nginx                          # Debian/Ubuntu

Sprawdzenie konfiguracji nginx:
sudo nginx -t                          # Test konfiguracji
sudo nginx -T                          # Pokaż pełną konfigurację

Sprawdzenie plików nginx:
ls -la /etc/nginx/
ls -la /var/log/nginx/
ls -la /usr/share/nginx/

Lokalizacja głównego pliku konfiguracyjnego:
cat /etc/nginx/nginx.conf

Sprawdzenie procesów nginx:
ps aux | grep nginx
pgrep nginx

Sprawdzenie portów nginx:
ss -tlnp | grep nginx
netstat -tlnp | grep nginx
lsof -i :80

Test działania:
curl localhost
curl -I localhost                      # Tylko headers
```

## 3. Sprawdź czy serwis nginx'a jest uruchomiony

```
Sprawdzenie statusu nginx:
systemctl status nginx

Krótkie sprawdzenie czy jest aktywny:
systemctl is-active nginx

Sprawdzenie czy jest włączony (autostart):
systemctl is-enabled nginx

Sprawdzenie czy działa:
systemctl is-running nginx

Szczegółowe informacje:
systemctl show nginx
systemctl show nginx -p ActiveState -p SubState

Sprawdzenie procesów:
ps aux | grep nginx
pgrep -l nginx

Sprawdzenie czy nasłuchuje na porcie:
ss -tlnp | grep :80
netstat -tlnp | grep :80

Test połączenia:
curl -s -o /dev/null -w "%{http_code}" localhost
wget --spider -q localhost && echo "OK" || echo "FAILED"

Sprawdzenie logów:
journalctl -u nginx --no-pager
tail /var/log/nginx/access.log
tail /var/log/nginx/error.log

Monitoring w czasie rzeczywistym:
journalctl -u nginx -f
systemctl status nginx -l
```

## 4. Zastopuj działanie serwisu nginx

```
Zatrzymanie serwisu nginx:
sudo systemctl stop nginx

Weryfikacja zatrzymania:
systemctl status nginx
systemctl is-active nginx

Sprawdzenie czy procesy zostały zatrzymane:
ps aux | grep nginx
pgrep nginx

Sprawdzenie czy porty są zwolnione:
ss -tlnp | grep :80
netstat -tlnp | grep :80

Test czy serwis nie odpowiada:
curl localhost
# Powinno pokazać błąd połączenia

Alternative metody zatrzymania:
sudo nginx -s stop                     # Natychmiastowe zatrzymanie
sudo nginx -s quit                     # Graceful shutdown
sudo nginx -s reload                   # Przeładowanie konfiguracji

Sprawdzenie w logach:
journalctl -u nginx --since "1 minute ago"
tail /var/log/nginx/error.log

Wymuszenie zatrzymania (jeśli normalne nie działa):
sudo systemctl kill nginx
sudo pkill nginx
```

## 5. Ponownie sprawdź czy serwis nginx'a jest uruchomiony

```
Sprawdzenie statusu po zatrzymaniu:
systemctl status nginx

Status powinien pokazać:
Active: inactive (dead)

Krótkie sprawdzenie:
systemctl is-active nginx
# Powinno zwrócić: inactive

Sprawdzenie procesów:
ps aux | grep nginx
pgrep nginx
# Nie powinno pokazać procesów nginx

Sprawdzenie portów:
ss -tlnp | grep :80
netstat -tlnp | grep :80
# Port 80 nie powinien być zajęty przez nginx

Test połączenia:
curl localhost
# Powinno pokazać błąd: Connection refused

Sprawdzenie w różny sposób:
systemctl is-running nginx             # inactive
systemctl show nginx -p ActiveState   # ActiveState=inactive

Logi zatrzymania:
journalctl -u nginx --since "2 minutes ago"
```

## 6. Uruchom serwis nginx'a i sprawdź czy działa

```
Uruchomienie nginx:
sudo systemctl start nginx

Sprawdzenie czy się uruchomił:
systemctl status nginx
systemctl is-active nginx              # Powinno zwrócić: active

Sprawdzenie procesów:
ps aux | grep nginx
pgrep -l nginx

Sprawdzenie portów:
ss -tlnp | grep :80
ss -tlnp | grep nginx

Test funkcjonalności:
curl localhost
curl -I localhost

Sprawdzenie w przeglądarce:
# Otwórz http://localhost lub http://IP_SERWERA

Sprawdzenie konfiguracji:
sudo nginx -t

Logi uruchomienia:
journalctl -u nginx --since "1 minute ago"
tail /var/log/nginx/access.log

Sprawdzenie wszystkich informacji:
systemctl show nginx -p ActiveState -p SubState -p Result

Test zaawansowany:
curl -s -o /dev/null -w "HTTP Code: %{http_code}\nTime: %{time_total}s\n" localhost
```

## 7. Włącz autostart serwisu nginx w trakcie startu systemu

```
Włączenie autostartu nginx:
sudo systemctl enable nginx

Sprawdzenie czy autostart jest włączony:
systemctl is-enabled nginx             # Powinno zwrócić: enabled

Lista wszystkich serwisów z autostartem:
systemctl list-unit-files --type=service --state=enabled

Sprawdzenie konkretnie nginx:
systemctl list-unit-files | grep nginx

Sprawdzenie symlinków (utworzonych przez enable):
ls -la /etc/systemd/system/multi-user.target.wants/ | grep nginx

Informacje o targecie:
systemctl list-dependencies nginx
systemctl show nginx -p WantedBy

Test autostartu (symulacja):
systemctl is-enabled nginx && echo "Uruchomi się automatycznie"

Sprawdzenie wszystkich enabled serwisów:
systemctl list-unit-files --state=enabled --no-pager

Wyłączenie autostartu (gdyby było potrzebne):
sudo systemctl disable nginx

Sprawdzenie dependency:
systemctl list-dependencies multi-user.target | grep nginx

Weryfikacja konfiguracji systemd:
systemctl daemon-reload                # Po zmianach w plikach unit
```

## 8. Sprawdź czy serwis firewalld jest włączony. Jeżeli tak to wyłącz i z poziomu przeglądarki wejdź na adres IP swojego serwera.

```
Sprawdzenie statusu firewalld:
systemctl status firewalld
systemctl is-active firewalld
systemctl is-enabled firewalld

Sprawdzenie konfiguracji firewall:
sudo firewall-cmd --state
sudo firewall-cmd --list-all

Sprawdzenie aktualnych reguł:
sudo firewall-cmd --list-services
sudo firewall-cmd --list-ports

Zatrzymanie firewalld:
sudo systemctl stop firewalld

Wyłączenie autostartu firewalld:
sudo systemctl disable firewalld

Weryfikacja wyłączenia:
systemctl status firewalld
systemctl is-active firewalld          # inactive
systemctl is-enabled firewalld         # disabled

Sprawdzenie czy porty są otwarte:
ss -tlnp | grep :80
nmap localhost -p 80

Sprawdzenie IP serwera:
ip addr show
hostname -I
curl ifconfig.me                       # Publiczne IP (jeśli dostępne)

Test z przeglądarki:
# Otwórz w przeglądarce:
# http://ADRES_IP_SERWERA
# http://localhost (jeśli lokalnie)

Test z curl:
curl http://ADRES_IP_SERWERA
curl -I http://ADRES_IP_SERWERA

Alternative - otwarcie portu zamiast wyłączania firewall:
sudo firewall-cmd --permanent --add-service=http
sudo firewall-cmd --permanent --add-port=80/tcp
sudo firewall-cmd --reload
sudo firewall-cmd --list-all

Sprawdzenie iptables (low-level):
sudo iptables -L
sudo iptables -t nat -L

Przywrócenie firewall (po testach):
sudo systemctl start firewalld
sudo systemctl enable firewalld
```

## Dodatkowe polecenia systemctl

```
Podstawowe operacje:
sudo systemctl start serwis            # Uruchom
sudo systemctl stop serwis             # Zatrzymaj
sudo systemctl restart serwis          # Restartuj
sudo systemctl reload serwis           # Przeładuj konfigurację
sudo systemctl enable serwis           # Włącz autostart
sudo systemctl disable serwis          # Wyłącz autostart

Informacje o serwisach:
systemctl status serwis                # Status
systemctl show serwis                  # Szczegóły
systemctl cat serwis                   # Pokaż plik unit
systemctl list-dependencies serwis     # Zależności

Zarządzanie systemem:
sudo systemctl daemon-reload           # Przeładuj konfigurację systemd
sudo systemctl reset-failed           # Resetuj failed units
systemctl list-units --failed         # Pokaż nieudane units

Cele systemowe (targets):
systemctl list-units --type=target     # Lista targets
systemctl get-default                  # Domyślny target
sudo systemctl set-default multi-user.target  # Ustaw domyślny

Logi i diagnostyka:
journalctl -u serwis                   # Logi serwisu
journalctl -u serwis -f               # Follow logs
journalctl -u serwis --since today    # Logi z dzisiaj
systemctl list-units --state=failed   # Serwisy z błędami

Tworzenie własnych serwisów:
# Przykład pliku /etc/systemd/system/moj-serwis.service
[Unit]
Description=Mój Custom Serwis
After=network.target

[Service]
Type=simple
ExecStart=/path/to/program
Restart=always
User=myuser

[Install]
WantedBy=multi-user.target
```