 **1. Czym jest yum?** 
 
```
System zarządzania pakietami dla systemów linuksowych używających systemu pakietów RPM
```

**2. Czym rózni się YUM od APT?**

```
Podstawową i najważniejszą różnicą jest to że znajduja się w innych dystrybucjach, resztę można przedstawić w tabelce: 
```

![Rozwiązania](/grafiki/1_04_8_1_aptvsrpm.png)

 **3. Wyświetl listę zainstalowanych przez managera yum paczek.**
``` 
sudo yum list installed
``` 

**4. W jakiej sytuacji zastosujesz manager pakietów yum a w jakiej rpm?**
```
Pakiet yum zainstaluje paczki z repozytorium a rpm z pliku lokalnego
```

**5. Gdzie znajduje się konfiguracja pliku yum.conf?**
```
Lokalizacja - /etc/yum.conf
```

**6. Czy za pośrednictwem manager pakietów yum jest moliwe pobieranie paczek z pominięciem kluczy gpg?**
```
Tak, wystarczy w pliku yum.conf wyłączyc opcje potwierdzania kluczy gpg
```

 **7. Gdzie znajdują się pliki repozytoriów skonfigurowanych dla yum?**
```
 lokalizacja /etc/yum.repos.d/
```

**8. Wymień najwazniejsze roznice pomiedzy managerem yum i dnf**
```
- Podczas usuwania pakietu manager DNF automatycznie usunie wszystkie pakiety zależności, które nie zostały specjalnie zainstalowane przez użytkownika.  
- Manager DNF nie chroni pakietów jądra. Oznacza to, że możesz usunąć pakiety jądra, nawet ten, który jest uruchomiony.
- Podczas aktualizacji przez manager DNF żaden pakiet zawierający nieistotne zależności nie zostanie zaktualizowany.  
```

 **9. Czym jest dependency hell?**
```
problem struktury linuksa bazujący na trudnym lub błędnym definiowaniu zależności między pakietami potrzebnymi do ich instalacji
```

**10. Czym się rózni polecenie yum update od yum upgrade?**
```
Polecenie yum upgrade wymusza usunięcie przestarzałych pakietów, podczas gdy yum update może, ale nie musi to robić. Usunięcie przestarzałych pakietów może być ryzykowne, ponieważ może usunąć pakiety, których używasz.
```

 **11. Wyszukaj w repozytorium paczkę "wget" oraz "mc"**
```
yum search wget mc
```

**12. Zainstaluj te pakiety ("wget" oraz "mc").**
```
 yum install wget mc
```

13.  **Bazując na informacjach zadnia 10 zaktualizuj pojedyńczy zainstalowany pakiet.**
```
sudo yum update pakiet
```

14.   **Wyświetl historie działań managera pakietów yum**
```
sudo yum history
```

15. **Wyczyś cache, metadane i nagłówki managera pakietów**.
```
yum clean all
```
