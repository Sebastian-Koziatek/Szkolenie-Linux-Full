# Rozwiązania - Managery pakietów

## 1. Czym jest YUM i jakie pełni funkcje w systemie Linux?

```
YUM (Yellowdog Updater Modified) to menedżer pakietów używany w dystrybucjach
opartych na Red Hat (RHEL, CentOS, Fedora starsze wersje).

Główne funkcje YUM:

Zarządzanie pakietami:
- Instalacja, aktualizacja i usuwanie pakietów
- Automatyczne rozwiązywanie zależności
- Weryfikacja integralności pakietów

Zarządzanie repozytoriami:
- Pobieranie metadanych z repozytoriów
- Wyszukiwanie pakietów w wielu repozytoriach
- Konfiguracja źródeł pakietów

Operacje systemowe:
- Aktualizacja całego systemu
- Grupowanie pakietów
- Historia transakcji
- Cache'owanie metadanych

Bezpieczeństwo:
- Weryfikacja podpisów GPG
- Sprawdzanie sum kontrolnych
- Rollback transakcji
```

## 2. Jakie są podstawowe różnice między YUM a APT?

```
YUM (Red Hat/CentOS/Fedora) vs APT (Debian/Ubuntu):

Format pakietów:
- YUM: pakiety RPM (.rpm)
- APT: pakiety DEB (.deb)

Pliki konfiguracyjne:
- YUM: /etc/yum.conf, /etc/yum.repos.d/
- APT: /etc/apt/sources.list, /etc/apt/sources.list.d/

Składnia komend:
- YUM: yum install package
- APT: apt install package / apt-get install package

Zarządzanie repozytoriami:
- YUM: pliki .repo w /etc/yum.repos.d/
- APT: wpisy w sources.list

Resolving dependencies:
- YUM: libsolv (nowsze), yum-resolver (starsze)
- APT: własny algorytm SAT solver

Cache:
- YUM: /var/cache/yum/
- APT: /var/cache/apt/

Narzędzia:
- YUM: rpm, yumdownloader, repoquery
- APT: dpkg, apt-cache, apt-file
```

## 3. Czym jest repozytorium pakietów i jaką pełni rolę?

```
Repozytorium pakietów to scentralizowane miejsce przechowywania pakietów
oprogramowania wraz z metadanymi.

Rola repozytoriów:

Dystrybucja oprogramowania:
- Centralne miejsce dla pakietów
- Weryfikowane i testowane oprogramowanie
- Różne kanały (stable, testing, updates)

Zarządzanie wersjami:
- Kontrola wersji pakietów
- Kompatybilność między pakietami
- Aktualizacje bezpieczeństwa

Metadane:
- Informacje o zależnościach
- Opisy pakietów
- Informacje o rozmiarze i architekturze

Bezpieczeństwo:
- Podpisy cyfrowe (GPG)
- Sumy kontrolne
- Weryfikacja pochodzenia

Typy repozytoriów:
- Oficjalne (base, updates, extras)
- Społecznościowe (EPEL, RPM Fusion)
- Firm trzecich (Google Chrome, Docker)
- Lokalne (własne organizacji)
```

## 4. Jak wyświetlić listę zainstalowanych pakietów za pomocą YUM?

```
Podstawowe komendy do wyświetlania zainstalowanych pakietów:

Wszystkie zainstalowane pakiety:
yum list installed

Z filtrowaniem po nazwie:
yum list installed | grep nazwa_pakietu
yum list installed nazwa_pakietu*

Szczegółowe informacje o zainstalowanych pakietach:
yum info zainstalowany_pakiet

Lista z informacją o rozmiarze:
rpm -qa --queryformat '%{NAME}-%{VERSION}-%{RELEASE} %{SIZE}\n' | sort

Tylko nazwy pakietów:
rpm -qa

Pakiety z określonego repozytorium:
yum list installed | grep @repo_name

Historia instalacji:
yum history list

Pakiety zainstalowane ręcznie (nie jako zależności):
yum mark showinstalled
```

## 5. W jakiej sytuacji użyjesz YUM, a kiedy RPM? Podaj praktyczne przykłady.

```
Użycie YUM:

Normalne zarządzanie pakietami:
- yum install httpd (automatyczne rozwiązywanie zależności)
- yum update (aktualizacja systemu)
- yum search apache (wyszukiwanie w repozytoriach)
- yum remove package (bezpieczne usuwanie z zależnościami)

Zarządzanie repozytoriami:
- yum repolist (lista repozytoriów)
- yum --enablerepo=epel install package

Użycie RPM:

Instalacja lokalnych pakietów:
- rpm -ivh package.rpm (gdy mamy lokalny plik .rpm)
- rpm -Uvh package.rpm (aktualizacja lokalnego pakietu)

Niska-poziomowe operacje:
- rpm -qa (szybkie listowanie bez dostępu do repozytoriów)
- rpm -qf /usr/bin/ls (które pakiet zawiera plik)
- rpm -ql package (lista plików w pakiecie)

Weryfikacja i diagnostyka:
- rpm -V package (weryfikacja integralności)
- rpm --verify package (sprawdzenie modyfikacji)
- rpm -qi package (informacje bez dostępu do sieci)

Scenariusze specjalne:
- Tryb rescue/single user (brak sieci)
- Niestandardowe pakiety firmowe
- Analiza forensyczna systemu
```

## 6. Gdzie znajduje się plik konfiguracyjny `yum.conf`? Jakie ustawienia można w nim zmienić?

```
Lokalizacja: /etc/yum.conf

Główne sekcje i ustawienia:

[main] - ustawienia globalne:

cachedir=/var/cache/yum/$basearch/$releasever
# Katalog cache'a

keepcache=0
# Czy zachowywać pobrane pakiety (0=nie, 1=tak)

debuglevel=2
# Poziom debugowania (0-10)

logfile=/var/log/yum.log
# Plik logów

exactarch=1
# Dokładne dopasowanie architektury

obsoletes=1
# Obsługa przestarzałych pakietów

gpgcheck=1
# Weryfikacja podpisów GPG

plugins=1
# Włączenie wtyczek

installonly_limit=5
# Limit pakietów kernel do zachowania

clean_requirements_on_remove=1
# Usuwanie nieużywanych zależności

Proxy settings:
proxy=http://proxy.company.com:3128
proxy_username=user
proxy_password=pass

Exclude packages:
exclude=kernel* php*

Timeout settings:
timeout=30
retries=10
```

## 7. Czy można pobierać pakiety z pominięciem weryfikacji kluczy GPG w YUM? Jeśli tak, to jak?

```
Tak, można pominąć weryfikację GPG, ale NIE JEST TO ZALECANE ze względów bezpieczeństwa.

Metody pomijania weryfikacji GPG:

1. Tymczasowo dla jednej komendy:
yum install --nogpgcheck package_name
yum update --nogpgcheck

2. Globalnie w /etc/yum.conf:
[main]
gpgcheck=0

3. Dla konkretnego repozytorium w /etc/yum.repos.d/repo.repo:
[reponame]
gpgcheck=0

4. Podczas instalacji lokalnego pakietu:
yum localinstall --nogpgcheck package.rpm
rpm -ivh --nocheck package.rpm

Zagrożenia bezpieczeństwa:
- Możliwość instalacji złośliwego oprogramowania
- Brak weryfikacji integralności pakietów
- Podatność na ataki man-in-the-middle
- Naruszenie polityk bezpieczeństwa organizacji

Lepsze rozwiązania:
- Import kluczy GPG: rpm --import GPG-KEY-FILE
- Konfiguracja zaufanych repozytoriów
- Używanie oficjalnych repozytoriów
- Weryfikacja kluczy przed importem
```

## 8. Gdzie przechowywane są pliki konfiguracyjne repozytoriów dla YUM?

```
Lokalizacje plików konfiguracyjnych repozytoriów:

Główny katalog: /etc/yum.repos.d/

Typowe pliki repozytoriów:
- CentOS-Base.repo (podstawowe repozytoria CentOS)
- epel.repo (Extra Packages for Enterprise Linux)
- rpmfusion-free.repo (RPM Fusion Free)
- docker-ce.repo (Docker Community Edition)

Struktura pliku .repo:

[repository-id]
name=Human Readable Name
baseurl=http://mirror.example.com/repo/
#mirrorlist=http://mirrorlist.example.com/
enabled=1
gpgcheck=1
gpgkey=file:///etc/pki/rpm-gpg/RPM-GPG-KEY-EPEL-7

Kluczowe parametry:

baseurl - bezpośredni URL do repozytorium
mirrorlist - URL do listy mirrorów
enabled - czy repozytorium jest aktywne (0/1)
gpgcheck - weryfikacja GPG (0/1)
gpgkey - ścieżka do klucza GPG
priority - priorytet repozytorium
exclude - wykluczenie pakietów
includepkgs - inkluzja tylko wybranych pakietów
cost - koszt repozytorium (dla optimization)

Zarządzanie repozytoriami:
yum repolist - lista aktywnych repozytoriów
yum repolist all - wszystkie repozytoria
yum-config-manager --enable repo-id
yum-config-manager --disable repo-id
```

## 9. Jakie są kluczowe różnice między YUM a jego następcą DNF?

```
DNF (Dandified YUM) zastąpił YUM w nowszych wersjach Fedora i RHEL 8+.

Główne różnice:

Wydajność:
- DNF: szybsze rozwiązywanie zależności (libsolv)
- YUM: wolniejszy, starszy solver
- DNF: lepsze wykorzystanie pamięci
- DNF: równoległy download pakietów

API i architektura:
- DNF: nowoczesne API Python 3
- YUM: starsze API Python 2
- DNF: modułowa architektura
- DNF: lepsze wsparcie dla wtyczek

Zarządzanie zależnościami:
- DNF: dokładniejsze rozwiązywanie konfliktów
- DNF: lepsze raportowanie problemów
- DNF: strict dependency checking
- YUM: czasami instalował niekompletne zależności

Kompatybilność komend:
- Większość komend jest identyczna
- DNF: dodatkowe komendy (dnf module)
- DNF: zmiana niektórych default behaviors
- Aliasy dla kompatybilności wstecznej

Nowe funkcje DNF:
- Modularność (AppStream)
- Lepsze cache'owanie
- Rich dependencies
- Boolean dependencies
- Improved documentation

Konfiguracja:
- DNF: /etc/dnf/dnf.conf
- YUM: /etc/yum.conf
- Podobna struktura repozytoriów
```

## 10. Czym jest „dependency hell" i w jaki sposób menedżery pakietów próbują go unikać?

```
"Dependency hell" to sytuacja, gdzie zarządzanie zależnościami
między pakietami staje się bardzo skomplikowane lub niemożliwe.

Przykłady problemów:

Konfliktujące zależności:
- Pakiet A wymaga biblioteki v1.0
- Pakiet B wymaga biblioteki v2.0 (niezgodnej z v1.0)

Circular dependencies:
- Pakiet A zależy od B
- Pakiet B zależy od A

Missing dependencies:
- Pakiet wymaga biblioteki niedostępnej w repozytorium

Version conflicts:
- Różne wersje tego samego pakietu wymagane jednocześnie

Sposoby unikania przez menedżery pakietów:

Automatyczne rozwiązywanie:
- SAT solvery (Boolean satisfiability)
- Algorytmy optymalizacyjne
- Detekcja konfliktów przed instalacją

Semantic versioning:
- Wersjonowanie zgodne z API
- Backward compatibility
- Clear dependency specification

Repozytoria:
- Kuratowane zbiory kompatybilnych pakietów
- Testing pipelines
- Quality assurance

Package isolation:
- Containers (Docker)
- Virtual environments (Python venv)
- Snap packages, Flatpak, AppImage
- Modules/AppStream (RHEL 8+)

Dependency tracking:
- Lock files
- Detailed dependency trees
- Rollback capabilities
```

## 11. Na czym polega różnica między `yum update` a `yum upgrade`?

```
W YUM komendy update i upgrade działają identycznie - są to aliasy.

yum update = yum upgrade

Obie komendy:
- Aktualizują wszystkie zainstalowane pakiety do najnowszych wersji
- Instalują nowe zależności jeśli potrzebne
- Zastępują przestarzałe pakiety (obsoletes)
- Aktualizują kernel do najnowszej wersji

Różnice w innych systemach:

APT (Debian/Ubuntu):
apt update - odświeża listę pakietów z repozytoriów
apt upgrade - aktualizuje pakiety (bez usuwania)
apt full-upgrade - aktualizuje z możliwością usuwania konfliktów

DNF:
dnf update - alias dla dnf upgrade
dnf upgrade - aktualizuje pakiety
dnf system-upgrade - aktualizacja całego systemu (major version)

Opcje dla YUM update/upgrade:

Aktualizacja konkretnego pakietu:
yum update package_name

Aktualizacja z wykluczeniami:
yum update --exclude=kernel*

Symulacja (bez wykonania):
yum update --assumeno
yum check-update

Bezpieczne aktualizacje:
yum update --security
yum update-minimal --security

Historia i rollback:
yum history
yum history undo ID
```

## 12. Jak wyszukać w repozytorium pakiety `wget` oraz `mc`?

```
Podstawowe wyszukiwanie pakietów:

Wyszukiwanie po nazwie:
yum search wget
yum search mc

Wyszukiwanie w nazwach i opisach:
yum search wget mc

Dokładne dopasowanie nazwy:
yum list wget
yum list mc

Informacje o pakiecie:
yum info wget
yum info mc

Wyszukiwanie zaawansowane:

Według dostawcy pliku:
yum provides */wget
yum whatprovides /usr/bin/mc

Wyszukiwanie w grupach:
yum grouplist
yum groupinfo "Development Tools"

Wyszukiwanie dostępnych wersji:
yum --showduplicates list wget

Filtrowanie po repozytorium:
yum --disablerepo="*" --enablerepo="base" search wget

Wyszukiwanie pakietów podobnych:
yum search "*wget*"
yum search file-manager

Sprawdzanie czy pakiet jest zainstalowany:
yum list installed wget
yum list installed mc

Z użyciem repoquery (jesli dostępne):
repoquery --whatprovides wget
repoquery -i mc
```

## 13. Jak zainstalować pakiety `wget` oraz `mc`?

```
Podstawowa instalacja:

Pojedyncze pakiety:
sudo yum install wget
sudo yum install mc

Wiele pakietów jednocześnie:
sudo yum install wget mc

Instalacja z potwierdzeniem:
sudo yum install -y wget mc

Opcje instalacji:

Z konkretnego repozytorium:
sudo yum --enablerepo=epel install mc
sudo yum install --enablerepo=extras wget

Instalacja bez zależności (niezalecane):
sudo yum install --nodeps wget

Symulacja instalacji:
yum install --assumeno wget mc
yum deplist wget mc

Instalacja lokalnego pakietu:
sudo yum localinstall wget-*.rpm
sudo yum install ./mc-*.rpm

Reinstalacja:
sudo yum reinstall wget
sudo yum reinstall mc

Instalacja konkretnej wersji:
sudo yum install wget-1.19.5
sudo yum downgrade wget

Grupowa instalacja:
sudo yum groupinstall "Development Tools"

Weryfikacja po instalacji:
which wget
which mc
wget --version
mc --version
```

## 14. Jak zaktualizować pojedynczy pakiet (np. `wget`) za pomocą YUM?

```
Aktualizacja pojedynczego pakietu:

Podstawowa komenda:
sudo yum update wget

Sprawdzenie dostępnych aktualizacji:
yum check-update wget
yum list updates wget

Aktualizacja z informacjami:
sudo yum update -v wget

Wymuszenie reinstalacji:
sudo yum reinstall wget

Aktualizacja do konkretnej wersji:
sudo yum update wget-1.20.1

Downgrade do starszej wersji:
sudo yum downgrade wget

Opcje aktualizacji:

Z wykluczeniem zależności:
sudo yum update --exclude=dependency_name wget

Z konkretnego repozytorium:
sudo yum --enablerepo=updates update wget

Symulacja aktualizacji:
yum update --assumeno wget

Historia przed aktualizacją:
yum history list wget

Informacje o pakiecie przed aktualizacją:
yum info wget
yum info available wget

Sprawdzenie zależności:
yum deplist wget

Aktualizacja bezpieczeństwa:
sudo yum update --security wget

Weryfikacja po aktualizacji:
yum info installed wget
rpm -qi wget
```

## 15. Jak wyświetlić historię operacji wykonanych przez YUM?

```
Podstawowe komendy historii:

Pełna lista transakcji:
yum history

Szczegóły konkretnej transakcji:
yum history info ID
yum history info 5

Lista według pakietu:
yum history list wget
yum history list all

Statystyki historii:
yum history stats

Operacje na historii:

Cofnięcie transakcji:
sudo yum history undo ID
sudo yum history undo 5

Powtórzenie transakcji:
sudo yum history redo ID

Rollback do poprzedniego stanu:
sudo yum history rollback ID

Szczegółowe informacje:

Pakiety w transakcji:
yum history package-list wget

Informacje o transakcji:
yum history info ID | grep -E "(Command|Return|Transaction)"

Nowe pakiety w transakcji:
yum history package-info wget

Wyszukiwanie w historii:
yum history list | grep install
yum history list | grep wget

Filtrowanie historii:

Według daty:
yum history list "last week"
yum history list "2023-01-01..2023-12-31"

Według użytkownika:
yum history list | grep root

Zarządzanie bazą historii:
yum history new
yum history sync

Lokalizacja plików historii:
/var/lib/yum/history/
```

## 16. Jak wyczyścić cache, metadane i nagłówki YUM?

```
Czyszczenie cache YUM:

Podstawowe komendy:
yum clean all          # Czyści wszystko
yum clean metadata     # Czyści metadane repozytoriów
yum clean packages     # Czyści pobrane pakiety
yum clean headers      # Czyści nagłówki
yum clean dbcache      # Czyści cache bazy danych

Szczegółowe opcje czyszczenia:

Cache repozytoriów:
yum clean expire-cache  # Wymusza odświeżenie cache
yum clean rpmdb        # Przebudowuje cache RPM DB

Konkretne repozytorium:
yum clean --enablerepo=epel all
yum --disablerepo="*" --enablerepo="base" clean metadata

Automatyczne czyszczenie:

Konfiguracja w /etc/yum.conf:
[main]
keepcache=0           # Nie zachowuj cache
clean_requirements_on_remove=1

Czyszczenie starych kerneli:
package-cleanup --oldkernels --count=2

Lokalizacje cache:
/var/cache/yum/       # Główny katalog cache
/var/cache/yum/$basearch/$releasever/

Sprawdzenie rozmiaru cache:
du -sh /var/cache/yum/

Czyszczenie manualne:
sudo rm -rf /var/cache/yum/*
sudo rm -rf /var/tmp/yum-*

Przebudowa cache:
yum makecache
yum makecache fast

Czyszczenie logów:
truncate -s 0 /var/log/yum.log

Optymalizacja po czyszczeniu:
yum check
rpm --rebuilddb
```

## 17. Przeanalizuj zależności wybranego pakietu (`yum deplist wget`) i spróbuj zrozumieć, co jest wymagane.

```
Analiza zależności pakietu wget:

Komenda analizy:
yum deplist wget

Przykładowe wyjście i interpretacja:

package: wget.x86_64 1.19.5-10.el8
  dependency: /bin/sh
    provider: bash.x86_64 4.4.20-1.el8_6
  dependency: libc.so.6()(64bit)
    provider: glibc.x86_64 2.28-164.el8
  dependency: libssl.so.1.1()(64bit)
    provider: openssl-libs.x86_64 1.1.1k-5.el8_5
  dependency: libcrypto.so.1.1()(64bit)
    provider: openssl-libs.x86_64 1.1.1k-5.el8_5

Interpretacja zależności:

/bin/sh (bash):
- Shell interpreter do uruchamiania skryptów
- Podstawowy komponent systemu
- Niezbędny do działania większości aplikacji

libc.so.6 (glibc):
- GNU C Library - podstawowa biblioteka C
- Zawiera fundamentalne funkcje systemowe
- malloc(), printf(), file I/O, networking

libssl.so.1.1 (OpenSSL):
- Biblioteka szyfrowania SSL/TLS
- Umożliwia bezpieczne połączenia HTTPS
- Kluczowa dla wget przy pobieraniu z HTTPS

libcrypto.so.1.1 (OpenSSL crypto):
- Kryptograficzne funkcje OpenSSL
- Hash functions, symmetric/asymmetric encryption
- Walidacja certyfikatów SSL

Dodatkowa analiza:

Sprawdzenie wszystkich zależności:
rpm -qR wget

Reverse dependencies (co zależy od wget):
yum whatrequires wget
repoquery --whatrequires wget

Zależności rekurencyjne:
yum deplist bash glibc openssl-libs

Sprawdzenie czy zależności są spełnione:
rpm -V wget
```

## 18. Porównaj polecenia `dnf` i `yum` dla tej samej operacji – które jest szybsze i bardziej informacyjne?

```
Porównanie wydajności i funkcjonalności DNF vs YUM:

Test instalacji pakietu:

YUM:
time yum install -y httpd
# Typowo: 15-30 sekund
# Mniej szczegółowe komunikaty o postępie

DNF:
time dnf install -y httpd
# Typowo: 10-20 sekund (szybsze)
# Bardziej szczegółowe informacje o postępie
# Lepsze formatowanie wyjścia

Wyszukiwanie pakietów:

YUM:
time yum search apache
# Wolniejsze przeszukiwanie metadanych
# Prostsze formatowanie wyników

DNF:
time dnf search apache
# Szybsze dzięki lepszemu indeksowaniu
# Bardziej informacyjne wyniki z opisami
# Lepsze kolorowanie składni

Rozwiązywanie zależności:

YUM:
yum deplist httpd
# Starszy solver, czasami nieprecyzyjny
# Może pomijać niektóre konflikty

DNF:
dnf repoquery --requires httpd
# Nowoczesny SAT solver (libsolv)
# Dokładniejsze rozwiązywanie konfliktów
# Lepsze raportowanie problemów

Informacje o pakietach:

YUM:
yum info httpd
# Podstawowe informacje

DNF:
dnf info httpd
# Bardziej szczegółowe informacje
# Lepsze formatowanie
# Dodatkowe metadane

Aktualizacja systemu:

YUM:
time yum update
# Wolniejsze pobieranie metadanych
# Mniejszy paralelizm

DNF:
time dnf upgrade
# Równoległy download pakietów
# Lepsze cache'owanie metadanych
# Szybsza weryfikacja GPG

Wnioski:

Szybkość: DNF wygrywa w większości operacji
Informacyjność: DNF dostarcza więcej szczegółów
Stabilność: YUM bardziej stabilny na starszych systemach
Kompatybilność: DNF zachowuje większość składni YUM
```