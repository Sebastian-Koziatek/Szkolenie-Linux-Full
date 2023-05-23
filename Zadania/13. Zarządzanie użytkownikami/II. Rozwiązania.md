1. Utwórz dwa dodatkowe konta użytkownika „tux1” i „tux2”. Nadaj tym użytkownikom hasło, aby móc się zalogować jako ci użytkownicy. Sprawdź, czy zostały utworzone konta użytkowników.
```
useradd tux1
useradd tux2
passwd tux1
passwd tux2
id tux1
id tux2
```

2. Przyjrzyj się różnym plikom przechowującym informacje o użytkownikach (/etc/passwd, /etc/shadow, /etc/group, /etc/gshadow), aby wyświetlić utworzone właśnie konta użytkowników.Spójrz także na katalog domowy tych nowych użytkowników, zawartość katalogu domowego i porównaj to z zawartością /etc/skel.
```
cat /etc/passwd
cat /etc/shadow
cat /etc/group
cat /etc/gshadow
```

**Plik /etc/gshadow może odczytać tylko użytkownik root i zawiera zaszyfrowane hasło dla każdej grupy, a także informacje o członkostwie w grupie i administratorze. Podobnie jak w pliku /etc/group, informacje o każdej grupie znajdują się w osobnym wierszu. Każdy z tych wierszy to rozdzielona dwukropkami.**

```
ls -ld /home/tux1
ls -la /home/tux1
ls -la /etc/skel
```

Katalog */etc/skel* zawiera pliki i katalogi, które są automatycznie kopiowane do nowego użytkownika podczas tworzenia go poleceniem useradd. Zapewni to wszystkim użytkownikom takie same ustawienia początkowe i środowisko.

3. W innym oknie terminala spróbuj zalogować się jako tux1 i tux2. czy to działa?
tak

4. Zablokuj konto użytkownika tux1.
```
usermod -L tux1 
```

5. W innym oknie terminala spróbuj zalogować się jako tux1. Czy możesz się teraz zalogwać?
```
 nie
```

  
6. Odblokuj konto użytkownika tux1.
```
usermod -U tux1
```

7. Zmodyfikuj parametry starzenia się hasła dla tux1 tak, aby przy następnym logowaniu tux1 był zmuszony zresetować swoje hasło.
```
chage -l tux1
chage tux1
chage -l tux1
```

8. Ponownie, w innym terminalu, zaloguj się jako tux1. czy to działa? Czy poproszono Cię o zmianę hasła?

9. Utwórz dodatkową grupę „pingwiny”. Uczyń użytkowników „tux1” i „tux2” członkami tej grupy.

```
groupadd pingwiny
usermod -a -G pingwiny tux1
usermod -a -G pingwiny tux2
```

10. Przyjrzyj się różnym plikom przechowującym informacje o użytkownikach, aby zobaczyć, jak administrowana jest ta grupa pomocnicza.
```
cat /etc/passwd
cat /etc/shadow
cat /etc/group
cat /etc/gshadow
id tux1
id tux2
```

11. Utwórz katalog grupy, /home/pingwiny. Ustaw odpowiednie uprawnienia w tym katalogu, aby użytkownicy tux1 i tux2 mogli pracować razem nad projektem w tym katalogu.
```
mkdir /home/pingwiny
chgrp pingwiny /home/pingwiny
```


Polecenie chgrp w systemie Linux służy do zmiany własności grupowej pliku lub katalogu. Wszystkie pliki w Linuksie należą do właściciela i grupy. Możesz ustawić właściciela za pomocą polecenia „chown”, a grupę za pomocą polecenia „chgrp”.

```
chmod 770 /home/pingwiny
```

[https://chmodcommand.com](https://chmodcommand.com/)

12. Zaloguj się jako tux1 i tux2 i sprawdź, czy rzeczywiście możesz używać tego katalogu do udostępniania dokumentów. Czy możecie też usuwać nawzajem dokumenty? Jak byś temu zapobiec?

```
chmod +t /home/pingwiny
```

13. Przejrzyj na informacje o starzeniu się hasła dla tux1.  
```
chage -lclear
```

14. Zobacz, ile procesów ma już twój użytkownik uruchomionych.

```
ps aux | grep tux1
```
  
Oprócz powłoki masz również proces ps i grep. Jeśli logujesz się przez ssh, istnieje również instancja demona sshd uruchomiona w Twoim imieniu. Więc normalnie na tym etapie masz uruchomione trzy lub cztery procesy.

Jeśli byłeś zalogowany przy użyciu środowiska graficznego, nie byłoby niczym niezwykłym zobaczyć na tym etapie około 20 procesów, w zależności od liczby otwartych okien. Przy twardym limicie ośmiu całkowicie niemożliwe byłoby korzystanie ze środowiska graficznego.

Spójrz na plik

cat /etc/security/limits i zawartość katalogu /etc/security/limits.d. Zmień parametry tux1 tak, aby miał miękki limit 5 i twardy limit 8 dla liczby procesów.:

```
tux1 soft nproc 2
tux1 hard nproc 4
```
