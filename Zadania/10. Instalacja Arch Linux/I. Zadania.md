1. Sprawdź jakie masz dostępne dyski w systemie.
2. Wykonaj partycjonowanie dysku i użyj "złotego podziału" (/boot, swap, /)

    1. cfdisk /dev/sda

3. Zdefniuj system plików ext4 dla partycji przeznaczonej na /boot i / oraz system plikow swap dla partycji przestrzeni wymiany

    1. mkfs.ext4 /dev/sda1

    2. mkfs.ext4 /dev/sda3

    3. mkswap /dev/sda2

4. Zamontuj dyski w poprawny sposób

    1. mount /dev/sda3 /mnt

    2. mkdir /mnt/boot

    3. mount /dev/sda1 /mnt/boot

    sda      8:0    0    30G  0 disk

    ├─sda1   8:1    0   977M  0 part /mnt/boot

    ├─sda2   8:2    0  15.6G  0 part [SWAP]

    └─sda3   8:3    0  13.4G  0 part /mnt

5. Zweryfikuj zamontowane dyski

    1. lsblk -l

6. Pobierz system i umieść go w katalogu /mnt, kernel i oprogramowanie którego będziemy potrzebować to (base base-devel linux linux-firmware)

    1. pacstrap -K /mnt base base-devel linux linux-firmware

7. Za pomocą polecenie genfstab wygeneruj plik konfiguracjny dysku /mnt/etc/fstab

    1. `genfstab -U -p /mnt >> /mnt/etc/fstab`

8. Sprawdź poprawnośc pliku /mnt/etc/fstab

    1. cat /mnt/etc/fstab

  

---

  

1. Następnie wejdź do przygotowanego systemu używająć polecenia arch-chroot

    1. `arch-chroot /mnt`

2. Zainstaluj za pomocą pacmana (managera pakietów) pakiet nano lub vi

    1. pacman -S nano vi

3. Skonfiguruj plik konfiguracyjny dla lokalizacyjny dla polskiej lokalizacji

    1. `nano /etc/locale.gen`

    2. ctrl + w

    3. pl_PL

4. Wygeneruj wytworzenie plików konfiguracyjnych w oparciu o konfiguracje z punktu 9 dla lokalizacji dla systemu

    1. locale-gen

5. Ustaw aby konsola obsługiwała polski język (/etc/locale.conf)

    1. `echo LANG=pl_PL.UTF-8 > /etc/locale.conf`

    2. `export LANG=pl_PL.UTF-8`

6. Załaduj polską klawiaturę i przełącz shell na język polski

    1. `loadkeys pl`

    2. `export LANG=pl_PL.UTF-8`

7. Stwórz plik konfiguracyjny dla konsoli (/etc/vconsole.conf)

    1. `KEYMAP=pl`

    2. `FONT=Lat2-Terminus16`

8. przejrzyj przygotowane pliki konfiguracyjne dla stref czasowych w folderze /usr/share/zoneinfo/Europe

    1. `ls /usr/share/zoneinfo/Europe`

9. Wykonaj dowiązanie miekkie do wskazanego pliku - ln -s /usr/share/zoneinfo/Europe/Warsaw /etc/localtime

    1. `ln -s /usr/share/zoneinfo/Europe/Warsaw /etc/localtime`

10. Wykonaj konfiguracje zegara sprzętowego (utc)

    1. hwclock --systohc --utc

11. Nadaj hostname dla swojej maszyny

    1. `echo szkolenie > /etc/hostname`

12. Wygeneruj "initrd" dla naszej przygotowanej konfiguracji

    1. `mkinitcpio -p linux`

13. Zainstaluj pakiet gruba

    1. pacman -S grub

14. Zainstaluj pliki konfiguracyjne gruba na dysku z którego będziemy bootwać system (dodaj opcje sprawdzenia poprawności)

    1. `grub-install --recheck /dev/sda`

15. Wygeneruj plik konfiguracyjny dla gruba

    1. `grub-mkconfig -o /boot/grub/grub.cfg`

16. Utwórz hasło do konta roota

    1. passwd

17. Utwórz nowego użytkownika i dodaj go do (audio,disk,floppy,games,lp,network,optical,power,storage,video,wheel)

    1. useradd -m -g users -G audio,disk,floppy,games,lp,network,optical,power,scanner,storage,video,wheel -s /bin/bash user

18. Zainstaluj ssh i włącz autostart daemona (serwisu)

    1. pacman -S openssh

    2. systemctl enable sshd

19. Zainstaluj klienta DHCP i włacz daemona (serwisu)

    pacman -S dhcpcd

    systemctl enable dhcpcd