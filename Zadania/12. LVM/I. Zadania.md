1.  Stwórz nowy dysk w virtualbox i przypisz mu przynajmniej 5GB  
2.  Sprawdź czy dysk jest widoczny w systmie
3.  Przeprowadź partycjonowanie dysku
4.  Utwórz na nowym dysku (/dev/sdc) nową partycję
5.  Stwórz PV z tej partycji
6.  Rozszerz grupę voluminów (VG) cs o nowy psychiczny volumen (PV)
7.  Sprawdź czy nowy psychiczny volumen został dodany do grupy volumenów
8.  Stwórz nowy volumen logiczny (LV) o nazwie szkolenie i wielkości 9GB w grupie volumenów cs
9.  Sprawdź czy twój volumen tam występuje w grupie volumenów cs
10.  Sprawdź czy ten volumen jest gdzieś zamontowany
[Zadanie opcjonalne]
11.  Stwórz w głownym katalogu systemowym folder szkolenie, przygotuj volumen szkolenie aby można go było zamontowac w stworzonym katalogu szkolenie i zamontuj go.