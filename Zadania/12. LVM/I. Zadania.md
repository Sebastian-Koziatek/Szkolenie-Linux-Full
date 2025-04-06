1.  Stwórz nowy dysk w virtualbox i przypisz mu przynajmniej 5GB  
2.  Sprawdź czy dysk jest widoczny w systmie
3.  Utwórz na nowym dysku (/dev/sdb) nową partycję
5.  Rozszerz grupę voluminów (VG) cs o nowy fizyczny volumen (PV)
6.  Sprawdź czy nowy psychiczny volumen został dodany do grupy volumenów
7.  Stwórz nowy volumen logiczny (LV) o nazwie szkolenie i wielkości 9GB w grupie volumenów cs
8.  Sprawdź czy twój volumen tam występuje w grupie volumenów cs
9.  Sprawdź czy ten volumen jest gdzieś zamontowany
[Zadanie opcjonalne]
10.  Stwórz w głownym katalogu systemowym folder szkolenie, przygotuj volumen szkolenie aby można go było zamontowac w stworzonym katalogu szkolenie i zamontuj go.
11. Wyjaśnij dlaczego używanie LVM bądź RAID jest zalecane i czym jest LVM.
12.  W jaki sposób zamontujesz katalog /var/log  na dysku /dev/sdb na partycji numer 3 dysku. Podaj poprawną komendę.
13.  Jak wyświetlić listę iistniejących grup woluminów?
14.  Jak wyświetlić listę dostępnych woluminów logicznych w systemie?
15. Jak wyświetlić listę dostępnych woluminów fizycznych w LVM?
16. Jak wyświetlić szczegółowe informacje o grupie woluminów?
17.  Jak wyświetlić szczegółowe informacje o woluminach logicznych?
18.  Jak zmienić nazwę grupy woluminów? czy możemy zmienić nazwę VG  aktualnie używanym systemie?  