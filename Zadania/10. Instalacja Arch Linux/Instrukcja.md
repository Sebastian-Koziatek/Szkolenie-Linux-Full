1. Sprawdź jakie masz dostępne dyski w systemie.
```
lsblk -l
```

2. Wykonaj partycjonowanie dysku i użyj "złotego podziału" (/boot, swap, /)
```
cfdisk /dev/sda
```

3. Zdefniuj system plików ext4 dla partycji przeznaczonej na /boot i / oraz system plikow swap dla partycji przestrzeni wymiany.
```
mkfs.ext4 /dev/sda1
mkfs.ext4 /dev/sda3
mkswap /dev/sda2
```

4. Zamontuj dyski w poprawny sposób
```
mount /dev/sda3 /mnt
mkdir /mnt/boot
mount /dev/sda1 /mnt/boot
```

5. Zweryfikuj zamontowane dyski
```
lsblk -l
```
zamontowane dyski powinny wyglądać tak
```
sda      8:0    0    30G  0 disk
├─sda1   8:1    0   977M  0 part /mnt/boot
├─sda2   8:2    0  15.6G  0 part [SWAP]
└─sda3   8:3    0  13.4G  0 part /mnt
```

6. Pobierz system i umieść go w katalogu /mnt, kernel i sterowniki których będziemy potrzebować do podstawowej instalacji systemu to (base base-devel linux linux-firmware).
```
pacstrap -K /mnt base base-devel linux linux-firmware
```

7. Za pomocą polecenie genfstab wygeneruj plik konfiguracjny dysku /mnt/etc/fstab
```
genfstab -U -p /mnt >> /mnt/etc/fstab
```

8. Sprawdź poprawnośc pliku /mnt/etc/fstab
```
cat /mnt/etc/fstab
```

9. Następnie wejdź do przygotowanego systemu używająć polecenia arch-chroot
```
arch-chroot /mnt
```

10. Zainstaluj za pomocą pacmana (managera pakietów) pakiet nano lub vi
```
pacman -S nano vi
```

11. Skonfiguruj plik konfiguracyjny dla lokalizacyjny dla polskiej lokalizacji
```
nano /etc/locale.gen

Wyszukaj w pliku frazy pl_PL
ctrl + w
pl_PL
Usuń znak # z przed pl_PL
ctrl + x
y
```

12. Wygeneruj wytworzenie lokalizacji systemu za pomoca plików konfiguracyjnych w oparciu o konfiguracje przygotowanej w poprzednim punktu 
```
 locale-gen
```

13. Ustaw lokalizacje klawiatury tak aby konsola obsługiwała polski język ***(/etc/locale.conf)***
```
echo LANG=pl_PL.UTF-8 > /etc/locale.conf
export LANG=pl_PL.UTF-8
```

14. Załaduj polską klawiaturę i przełącz shell na język polski
```
loadkeys pl
export LANG=pl_PL.UTF-8
```

15. Stwórz plik konfiguracyjny dla konsoli (/etc/vconsole.conf)
```
KEYMAP=pl
FONT=Lat2-Terminus16
```

16. Przejrzyj przygotowane pliki konfiguracyjne dla stref czasowych w folderze ***/usr/share/zoneinfo/Europe***
```
ls /usr/share/zoneinfo/Europe
```

17. Wykonaj dowiązanie miekkie do wskazanego pliku - ln -s /usr/share/zoneinfo/Europe/Warsaw /etc/localtime

```
ln -s /usr/share/zoneinfo/Europe/Warsaw /etc/localtime
```

18. Wykonaj konfiguracje zegara sprzętowego (utc)
```
hwclock --systohc --utc
```

19. Nadaj nazwe (hostname) dla swojej maszyny
```
echo szkolenie > /etc/hostname
```

20. Wygeneruj "initrd" dla naszej przygotowanej konfiguracji
```
mkinitcpio -p linux
```

21. Zainstaluj pakiet gruba
```
 pacman -S grub
```

22. Zainstaluj pliki konfiguracyjne gruba na dysku z którego będziemy bootwać system (dodaj opcje sprawdzenia poprawności)
```
grub-install --recheck /dev/sda
```

23. Wygeneruj plik konfiguracyjny dla gruba
```
grub-mkconfig -o /boot/grub/grub.cfg
```

24. Utwórz hasło do konta roota
```
passwd
```

25. Utwórz nowego użytkownika i dodaj go do grup:(audio,disk,floppy,games,lp,network,optical,power,storage,video,wheel)
   ```
 useradd -m -g users -G audio,disk,floppy,games,lp,network,optical,power,scanner,storage,video,wheel -s /bin/bash nazwa_uzytkownika
```

26. Zainstaluj ssh i włącz autostart daemona (serwisu)
```
pacman -S openssh
systemctl enable sshd
```

27. Zainstaluj klienta DHCP i włacz daemona (serwisu)
```
pacman -S dhcpcd
systemctl enable dhcpcd
```