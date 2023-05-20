1.  Stwórz nowy dysk w virtualbox i przypisz mu przynajmniej 10GB  

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

4.  Stwórz PV z tej partycji
```
sudo vgextend cs /dev/sdb1
```

5.  Rozszerz grupę voluminów (VG) cs o nowy psychiczny volumen (PV)
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

[Zadanie opcjonalne]
10.  Stwórz w głownym katalogu systemowym folder szkolenie, przygotuj volumen szkolenie aby można go było zamontowac w stworzonym katalogu szkolenie i zamontuj go.

```
mkdir /szkolenie
mkfs.ext4 /dev/cs/szkolenie
mount /dev/cs/szkolenie /root/szkolenie/
```