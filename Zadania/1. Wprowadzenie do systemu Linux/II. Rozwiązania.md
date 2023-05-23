1.  **Czym jest Linux?**
```
Linux - otwarty system operacy stworzony w oparciu o UNIX. 
```

2.  **Czym jest dystrybucja Linuksa?**
```
Kompletny system operacyjny zbudowany na bazie jądra Linux. Zawiera podstawy zestaw programów do obslugi systemu.
```

3.  **Czym się rónią się - zwykła dystrybucja, dystrybucja LTS oraz dystrybucja Rolling Release?**
```
Dystrybucja zwykła to dystrybucja w której całe wydanie jest wersjonowane i aktualizacja takiej dystrybucji oznacza zmiane wersji na nowej. 

LTS to Long Term Support i określa dystrybucje długo wspieraną, tak jak w przypadku zwykłej dystrybucji aktualizacja oznacza zmianę wersji na nowej, jedyna różnica to wydłuzony czas wsparcia. 

Rolling Release opiera się na aktualizacji paczek bez konieczności aktualizacji wersji systemu. Na ogół takie dystrybucje bazują na najnowszych paczkach pakietów.
```

4.  **Czy dystrybucje ARM da się zainstalowac na architekturze x86?**
```
W normalny sposób nie.
```

5.  **Czym się róni Desktop envoirment od Windows Managera?**
```
Desktop envoirment działa w innej warstwie systemu i wymaga silnika (xorg/wayland) do uruchomienia podczas gdy Windows Manager działa w wyżej warstwie i nie potrzebuje do uruchomienia żadnego silnika
```

6.  **Wymień trzy zalety pracy w trybie wiersza poleceń.**
```
Bardzo duża precyzja pracy
Brak kolejnej warstwy	
Szybsze wykonywanie czynności
```

7.  **Wymien trzy zalety i trzy wady pracy w środowisku graficznym.**
```
Zalety:
Możliwość używania myszki
Możliwość konfiguracji wyglądu
Początkowo łatwiejsze do używania

Wady:
Najmniej stabilna część systemu
Wytworzenie dodatkowej warstwy
Najbardziej awaryjna część systemu
```

8.  ***Czym jest pamięc SWAP i jakie wartości powinna przybrac?***
```
Jest to partycja wymiany która służy do tymczasowego przechowywania danych
```

9.  **Co się stanie w przypadku systemu który nie posiada zadeklarowanej pamięci SWAP lub jest ona wyłączona?** 
```
Dane będą po prostu bezpośrednio cachowane przez dysk z pominieciem pamięci SWAP
```