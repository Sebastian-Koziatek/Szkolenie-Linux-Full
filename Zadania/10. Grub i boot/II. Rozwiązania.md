# Rozwiązania - Grub i boot

## 1. Przejrzyj plik konfiguracyjny i sprawdź jakie ma opcje /etc/default/grub

```
Wyświetlenie pliku konfiguracyjnego GRUB:
cat /etc/default/grub

Główne opcje w /etc/default/grub:

GRUB_TIMEOUT=5
# Czas oczekiwania na wybór systemu (sekundy)

GRUB_DISTRIBUTOR="$(sed 's, release .*$,,g' /etc/system-release)"
# Nazwa dystrybucji wyświetlana w menu

GRUB_DEFAULT=saved
# Domyślny wpis do uruchomienia
# 0 = pierwszy wpis, saved = ostatnio wybrany

GRUB_DISABLE_SUBMENU=true
# Wyłącza podmenu (wszystkie kernele w głównym menu)

GRUB_TERMINAL_OUTPUT="console"
# Typ terminala wyjściowego

GRUB_CMDLINE_LINUX="crashkernel=auto rhgb quiet"
# Parametry kernela przekazywane podczas startu
# rhgb = Red Hat Graphical Boot
# quiet = ograniczone komunikaty podczas startu

GRUB_DISABLE_RECOVERY="true"
# Wyłącza opcje recovery mode

Edycja konfiguracji:
sudo nano /etc/default/grub

Po zmianach regeneruj konfigurację:
sudo grub2-mkconfig -o /boot/grub2/grub.cfg

Dodatkowe opcje:
GRUB_TIMEOUT_STYLE=menu     # Styl wyświetlania timeout
GRUB_GFXMODE=auto          # Rozdzielczość graficzna
GRUB_DISABLE_OS_PROBER=true # Wyłącz szukanie innych OS
GRUB_SAVEDEFAULT=true      # Zapisuj ostatni wybór jako domyślny
```

## 2. Sprawdź pliki znajdujące się na partycji /boot, co tam możesz znaleźć?

```
Lista zawartości /boot:
ls -la /boot/

Główne pliki i katalogi w /boot:

grub2/
# Katalog z konfiguracją GRUB2
ls -la /boot/grub2/

vmlinuz-*
# Skompresowane obrazy kernela
ls -la /boot/vmlinuz-*

initramfs-*
# Initial RAM filesystem - sterowniki potrzebne do startu
ls -la /boot/initramfs-*

config-*
# Konfiguracja kompilacji kernela
ls -la /boot/config-*

System.map-*
# Mapowanie symboli kernela (debugowanie)
ls -la /boot/System.map-*

efi/ (jeśli system używa UEFI)
# Pliki UEFI
ls -la /boot/efi/

Szczegółowa analiza:
du -sh /boot/*                    # Rozmiary plików
file /boot/vmlinuz-*             # Typ plików kernela
file /boot/initramfs-*           # Typ plików initramfs

Sprawdzenie konfiguracji GRUB:
cat /boot/grub2/grub.cfg | head -20

Sprawdzenie systemu plików /boot:
df -h /boot
mount | grep boot
lsblk | grep boot

Weryfikacja integralności:
rpm -V kernel
rpm -qa | grep kernel
```

## 3. Użyj polecenia rpm, aby stworzyć listę wszystkich zainstalowanych kerneli w twoim systemie.

```
Lista zainstalowanych kerneli:
rpm -qa kernel*

Sortowanie według daty instalacji:
rpm -qa kernel* --last

Szczegółowe informacje o kernelach:
rpm -qi kernel
rpm -qa kernel* | xargs rpm -qi

Lista wszystkich pakietów związanych z kerelem:
rpm -qa | grep kernel

Sprawdzenie plików zainstalowanych przez kernel:
rpm -ql kernel-$(uname -r)

Weryfikacja pakietów kernel:
rpm -V kernel-$(uname -r)

Informacje o rozmiarze:
rpm -qa kernel* --queryformat '%{NAME}-%{VERSION}-%{RELEASE} %{SIZE}\n'

Historia instalacji kerneli:
rpm -qa kernel* --last | head -10

Sprawdzenie zależności kernela:
rpm -qR kernel-$(uname -r)

Alternative z dnf:
dnf list installed kernel*
dnf history | grep kernel

Sprawdzenie dostępnych kerneli:
dnf list available kernel*

Porównanie wersji:
rpm -qa kernel* | sort -V
```

## 4. Sprawdź wersję jądra, która jest aktualnie uruchomiona.

```
Podstawowe polecenie:
uname -r

Szczegółowe informacje o kernelu:
uname -a

Wersja kernela z dodatkowymi informacjami:
cat /proc/version

Informacje o kompilacji kernela:
uname -v

Architektura systemu:
uname -m

Nazwa systemu:
uname -s

Wszystkie informacje systemowe:
hostnamectl

Sprawdzenie w /proc:
cat /proc/sys/kernel/osrelease
cat /proc/sys/kernel/version

Porównanie z zainstalowanymi:
echo "Uruchomiony: $(uname -r)"
echo "Zainstalowane:"
rpm -qa kernel* | sort

Sprawdzenie czy to najnowszy kernel:
latest_kernel=$(rpm -qa kernel --last | head -1 | cut -d' ' -f1)
current_kernel="kernel-$(uname -r)"
echo "Najnowszy: $latest_kernel"
echo "Aktualny: $current_kernel"

Informacje z dmesg:
dmesg | grep -i "Linux version"

Sprawdzenie uptime:
uptime
cat /proc/uptime
```

## 5. Sprawdź listę aktualnie załadowanych modułów.

```
Lista wszystkich załadowanych modułów:
lsmod

Sortowanie według nazwy:
lsmod | sort

Liczba załadowanych modułów:
lsmod | wc -l

Szczegółowe informacje o module:
modinfo nazwa_modulu

Przykład szczegółowych informacji:
modinfo e1000e    # Sterownik karty sieciowej
modinfo ext4      # System plików

Sprawdzenie czy moduł jest załadowany:
lsmod | grep nazwa_modulu

Informacje o module z /proc:
cat /proc/modules

Sprawdzenie zależności modułów:
modprobe --show-depends nazwa_modulu

Drzewo zależności:
modprobe --show-depends e1000e

Ładowanie/usuwanie modułów:
sudo modprobe nazwa_modulu      # Załaduj
sudo modprobe -r nazwa_modulu   # Usuń

Sprawdzenie dostępnych modułów:
find /lib/modules/$(uname -r) -name "*.ko" | wc -l

Moduły kernela według kategorii:
ls /lib/modules/$(uname -r)/kernel/

Sprawdzenie blacklisted modułów:
cat /etc/modprobe.d/blacklist.conf

Moduły załadowane podczas startu:
dmesg | grep -i "module"

Statystyki modułów:
cat /proc/modules | awk '{print $1, $2}' | sort -k2 -nr

Sprawdzenie parametrów modułu:
cat /sys/module/nazwa_modulu/parameters/*

Historia ładowania modułów:
journalctl -k | grep -i module
```

## Dodatkowe informacje o GRUB i boot

```
Zarządzanie GRUB:

Sprawdzenie wersji GRUB:
grub2-install --version

Regeneracja konfiguracji:
sudo grub2-mkconfig -o /boot/grub2/grub.cfg

Ustawienie domyślnego wpisu:
sudo grub2-set-default 0

Sprawdzenie domyślnego wpisu:
grub2-editenv list

UEFI vs BIOS:
# UEFI:
ls /sys/firmware/efi
efibootmgr -v

# BIOS:
sudo grub2-install /dev/sda

Bootloader rescue:
# Jeśli system nie startuje:
# 1. Boot z LiveCD/USB
# 2. Mount partycji root
# 3. chroot do systemu
# 4. Regeneruj GRUB

Sprawdzenie czasu startu:
systemd-analyze
systemd-analyze blame
systemd-analyze critical-chain

Informacje o initramfs:
lsinitrd /boot/initramfs-$(uname -r).img | head -20

Regeneracja initramfs:
sudo dracut --force --verbose

Diagnostyka startu:
journalctl -b    # Logi z ostatniego startu
dmesg           # Komunikaty kernela
```