# Rozwiązania - Wprowadzenie do systemu Linux

## 1. Na jakich platformach sprzętowych można uruchomić Linuksa?

```
Linux może być uruchomiony na szerokim spektrum platform sprzętowych:

- x86_64 (AMD64) - najczęściej używana architektura na komputerach stacjonarnych i serwerach
- x86 (32-bit) - starsze komputery osobiste
- ARM - urządzenia mobilne, tablety, Raspberry Pi, routery
- ARM64 (AArch64) - nowsze procesory ARM w serwerach i komputerach
- PowerPC - starsze komputery Mac, serwery IBM
- SPARC - serwery Sun/Oracle
- MIPS - routery, systemy wbudowane
- RISC-V - nowa otwarta architektura
- s390x - mainframe'y IBM
- IA-64 (Itanium) - serwery HP/Intel (wycofane)
- Alpha - starsze serwery DEC/Compaq/HP
```

## 2. Jak wybrać odpowiednią wersję systemu Linux do swoich potrzeb?

```
Wybór dystrybucji Linux zależy od kilku kluczowych czynników:

Cel użytkowania:
- Desktop/laptop osobisty: Ubuntu, Linux Mint, Fedora, openSUSE
- Serwer: RHEL, CentOS Stream, Ubuntu Server, Debian
- Systemy wbudowane: Yocto, OpenWrt, Alpine Linux
- Bezpieczeństwo: Kali Linux, Parrot Security OS
- Nauka: CentOS Stream, Ubuntu, Fedora

Poziom doświadczenia:
- Początkujący: Ubuntu, Linux Mint, Pop!_OS
- Średnio zaawansowany: Fedora, openSUSE, Debian
- Zaawansowany: Arch Linux, Gentoo, LFS

Model wsparcia:
- Wsparcie komercyjne: RHEL, SLES, Ubuntu Pro
- Wsparcie społeczności: Fedora, openSUSE, Debian
- Długie wsparcie (LTS): Ubuntu LTS, RHEL, SLES

Środowisko docelowe:
- Przedsiębiorstwo: RHEL, SLES, Ubuntu Pro
- Chmura: Amazon Linux, Google Container-Optimized OS
- Kontenery: Alpine Linux, CoreOS
```

## 3. Czym różnią się od siebie dystrybucje: RHEL, CentOS i CentOS Stream?

```
RHEL (Red Hat Enterprise Linux):
- Komercyjna dystrybucja Red Hat
- Płatne wsparcie techniczne i aktualizacje bezpieczeństwa
- Długie cykle wsparcia (10+ lat)
- Certyfikacje i zgodność z normami korporacyjnymi
- Stabilność i niezawodność dla środowisk produkcyjnych

CentOS (Community Enterprise Operating System):
- Darmowa dystrybucja oparta na kodzie źródłowym RHEL
- Identyczna funkcjonalność z RHEL, ale bez wsparcia komercyjnego
- Wsparcie społeczności
- Projekt zakończony w 2021 roku na rzecz CentOS Stream

CentOS Stream:
- "Upstream" dla RHEL - testowa wersja przed RHEL
- Aktualizacje są bardziej częste niż w RHEL
- Przeznaczona dla deweloperów i testerów
- Darmowa z wsparciem społeczności
- Rolling release model z punktami stabilności
- Zastąpiła tradycyjną dystrybucję CentOS
```

## 4. Jak przebiega typowa instalacja systemu Linux?

```
Typowa instalacja systemu Linux składa się z następujących etapów:

1. Przygotowanie medium instalacyjnego:
   - Pobranie obrazu ISO dystrybucji
   - Utworzenie bootowalnego USB/DVD

2. Boot z medium instalacyjnego:
   - Konfiguracja BIOS/UEFI
   - Wybór opcji instalacji (tryb graficzny/tekstowy)

3. Wybór języka i lokalizacji:
   - Ustawienie języka systemu
   - Strefa czasowa
   - Układ klawiatury

4. Partycjonowanie dysku:
   - Automatyczne lub ręczne
   - Utworzenie partycji root (/), home, swap
   - Wybór systemu plików (ext4, xfs, btrfs)

5. Konfiguracja sieci:
   - Ustawienia IP (DHCP/statyczne)
   - Nazwa hosta

6. Tworzenie konta użytkownika:
   - Konto administratora (root)
   - Konto użytkownika podstawowego

7. Wybór oprogramowania:
   - Środowisko graficzne
   - Dodatkowe pakiety

8. Instalacja systemu:
   - Kopiowanie plików
   - Konfiguracja bootloadera (GRUB)

9. Restart i pierwsza konfiguracja
```

## 5. Czym jest SWAP i jakie są różnice między jego włączeniem a wyłączeniem?

```
SWAP (przestrzeń wymiany) to obszar na dysku używany jako dodatkowa pamięć wirtualna.

Z SWAP:
Zalety:
- Możliwość uruchomienia aplikacji wymagających więcej RAM niż dostępne
- Ochrona przed zabiciem procesów przy braku pamięci
- Umożliwia hibernację systemu
- Lepsze zarządzanie pamięcią przez kernel

Wady:
- Znaczne spowolnienie przy intensywnym używaniu
- Zużycie przestrzeni dyskowej
- Dodatkowe operacje I/O na dysku

Bez SWAP:
Zalety:
- Lepsze wydajności - brak spowolnień dyskowych
- Oszczędność miejsca na dysku
- Zmuszenie do lepszej optymalizacji pamięci

Wady:
- Ryzyko zabicia procesów przy braku RAM (OOM Killer)
- Brak możliwości hibernacji
- Ograniczenia w uruchamianiu aplikacji wymagających dużo pamięci
- Potencjalne crashes systemu przy wyczerpaniu RAM
```

## 6. Jak dobrać odpowiedni rozmiar partycji SWAP do swojego systemu?

```
Wytyczne doboru rozmiaru SWAP:

Tradycyjne zasady:
- RAM ≤ 2GB: SWAP = 2 × RAM
- RAM 2-8GB: SWAP = RAM
- RAM 8-64GB: SWAP = 0.5 × RAM
- RAM > 64GB: SWAP = 4-8GB (lub 0 jeśli nie potrzeba hibernacji)

Nowoczesne podejście:
- SSD + dużo RAM (16GB+): 2-4GB lub brak SWAP
- Serwery: minimalne SWAP (2-4GB) jako zabezpieczenie
- Desktop z hibernacją: SWAP ≥ RAM
- Systemy z ograniczoną przestrzenią: brak SWAP

Czynniki do rozważenia:
- Typ dysku (HDD vs SSD)
- Wzorce użytkowania pamięci
- Potrzeba hibernacji
- Dostępna przestrzeń dyskowa
- Typ obciążenia (desktop vs serwer)

Alternatywy:
- ZRAM - kompresja RAM zamiast SWAP na dysku
- Swap file zamiast partycji (łatwiejsza zmiana rozmiaru)
```

## 7. Czym różni się środowisko graficzne (Desktop Environment) od menedżera okien (Window Manager)?

```
Desktop Environment (DE):
- Kompletny pakiet graficzny zawierający wiele komponentów
- Zawiera: menedżer okien, panel, menadżer plików, aplikacje systemowe
- Przykłady: GNOME, KDE Plasma, XFCE, Cinnamon, MATE
- Zapewnia spójny wygląd i zachowanie
- Więcej zasobów systemowych
- Łatwiejszy dla początkujących
- Większa integracja między aplikacjami

Window Manager (WM):
- Tylko zarządza oknami i ich rozmieszczeniem
- Kontroluje: pozycję, rozmiar, dekoracje okien
- Przykłady: i3, dwm, awesome, openbox, bspwm
- Minimalne zużycie zasobów
- Większa konfigurowalność
- Wymaga dodatkowych aplikacji (panel, launcher)
- Bardziej dla zaawansowanych użytkowników

Typy Window Managerów:
- Stacking (tradycyjne): okna nakładają się
- Tiling: okna automatycznie wypełniają ekran
- Dynamic: kombinacja stacking i tiling
- Compositing: efekty wizualne, przezroczystość
```

## 8. Jakie są główne zalety korzystania z CLI (Command Line Interface) w porównaniu do GUI?

```
Zalety CLI:

Wydajność:
- Szybsze wykonywanie zadań dla doświadczonych użytkowników
- Bezpośredni dostęp do funkcji systemu
- Minimalne zużycie zasobów systemowych

Automatyzacja:
- Łatwe tworzenie skryptów
- Batch processing wielu plików
- Integracja z systemami CI/CD

Precyzja i kontrola:
- Dokładne parametry poleceń
- Większa kontrola nad operacjami
- Dostęp do zaawansowanych funkcji

Zdalny dostęp:
- Praca przez SSH z minimalnym transferem danych
- Administracja serwerów bez GUI
- Działanie w środowiskach o ograniczonej przepustowości

Stabilność:
- Rzadsze zawieszanie się
- Działanie w trybie recovery
- Mniejsze wymagania sprzętowe

Elastyczność:
- Łączenie komend (pipes, redirection)
- Powerful text processing tools
- Praca z wieloma sesjami jednocześnie

Dokumentacja:
- Łatwy dostęp do help i manual pages
- Historia komend
- Reprodukowalne operacje
```

## 9. Wymień po 3 zalety i 3 wady środowiska graficznego (GUI).

```
Zalety GUI:

1. Intuicyjność i łatwość użytkowania:
   - Wizualna reprezentacja plików i folderów
   - Drag & drop operations
   - Ikony i menu ułatwiające nawigację

2. Multitasking wizualny:
   - Łatwe przełączanie między aplikacjami
   - Podgląd wielu okien jednocześnie
   - Workspace/virtual desktop management

3. Dostępność dla początkujących:
   - Niski próg wejścia
   - Kontekstowe menu i tooltips
   - Standardowe konwencje interfejsu

Wady GUI:

1. Zużycie zasobów:
   - Wysokie wykorzystanie RAM i CPU
   - Wymagania graficzne (GPU)
   - Większe zużycie baterii na laptopach

2. Ograniczona automatyzacja:
   - Trudności w skryptowaniu
   - Powolne wykonywanie powtarzalnych zadań
   - Zależność od interakcji użytkownika

3. Problemy z administracją zdalną:
   - Wymaganie X11 forwarding lub VNC/RDP
   - Większe wymagania przepustowości
   - Potencjalne problemy z bezpieczeństwem przy zdalnym dostępie
```