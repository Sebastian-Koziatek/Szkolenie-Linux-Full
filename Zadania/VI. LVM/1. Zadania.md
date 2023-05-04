1.  Stwórz nowy dysk w virtualbox i przypisz mu przynajmniej 5GB  
2.  Utwórz na nowym dysku (/dev/sdc) nową partycję
3.  Stwórz PV z tej partycji
4.  Rozszerz grupę voluminów (VG) cs o nowy psychiczny volumen (PV)
5.  Sprawdź czy nowy psychiczny volumen został dodany do grupy volumenów
6.  Stwórz nowy volumen logiczny (LV) o nazwie szkolenie i wielkości 9GB w grupie volumenów cs
7.  Sprawdź czy twój volumen tam występuje w grupie volumenów cs
8.  Sprawdź czy ten volumen jest gdzieś zamontowany