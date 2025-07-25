1.  Stwórz nowy dysk w virtualbox i przypisz mu 20GB  

2. Sprawdź czy dysk jest widoczny w systmie
```
lsblk -l
```

3.  Przeprowadź partycjonowanie dysku - stwórz jedną  partycję zajmującą całą pamięc dysku
```
cfdisk
```

4. Utwórz na nowym dysku (/dev/sdc) nową partycję
```
pvcreate /dev/sdb1
```

5.  Stwórz PV z tej partycji
```
sudo vgextend cs /dev/sdb1
```

6.  Sprawdź czy nowy psychiczny volumen został dodany do grupy volumenów
```
sudo pvscan
sudo vgdisplay
```

7.  Stwórz nowy volumen logiczny (LV) o nazwie szkolenie i wielkości 9GB w grupie volumenów cs
```
sudo lvcreate -n szkolenie --size 9G cs
```

8.  Sprawdź czy twój volumen tam występuje w grupie volumenów cs
```
sudo lvmdiskscan
lsblk
```

9.  Sprawdź czy ten volumen jest gdzieś zamontowany
```
lsblk -l
```

10.  Stwórz w głownym katalogu systemowym folder szkolenie, przygotuj volumen szkolenie aby można go było zamontowac w stworzonym katalogu szkolenie i zamontuj go.
```
mkdir /szkolenie
mkfs.ext4 /dev/cs/szkolenie
mount /dev/cs/szkolenie /root/szkolenie/
```

11. Wyjaśnij dlaczego używanie LVM bądź RAID jest zalecane i czym jest LVM.
```
LVM to skrót od Large Volume Management, jest to urządzenie do zarządzania pamięcią masową. Użytkownicy mogą tworzyć, zmieniać rozmiar i usuwać partycje LVM. Zwiększa, elastyczność i kontrolę. LVM służy do gromadzenia istniejących urządzeń pamięci masowej w grupy i przydzielania jednostek logicznych.
```

12.  W jaki sposób zamontujesz katalog /var/log  na dysku /dev/sdb na partycji numer 3 dysku. Podaj poprawną komendę.
```
mount /dev/sdb3 /var/log
```

13.  Jak wyświetlić listę iistniejących grup woluminów?
```
vgs
```

14.  Jak wyświetlić listę dostępnych woluminów logicznych w systemie?
```
lvs
```

15. Jak wyświetlić listę dostępnych woluminów fizycznych w LVM?
```
pvs
```

16. Jak wyświetlić szczegółowe informacje o grupie woluminów?
```
vgdisplay  vg_name
```

17.  Jak wyświetlić szczegółowe informacje o woluminach logicznych?
```
lvdisplay  /dev/vg_name/lv_name
```

18.  Jak zmienić nazwę grupy woluminów? czy możemy zmienić nazwę VG  aktualnie używanym systemie?  
```
Odpowiedź:Tak. Można zmienić nazwę grupy woluminów w locie. Ale zamontowane woluminy nie będą odzwierciedlać tego samego, chyba że ponownie zamontujesz wolumin z nową nazwą VG.
Musisz zaktualizować /etc/fstab o nową nazwę VG, aby zamontować woluminy podczas ponownego 
```