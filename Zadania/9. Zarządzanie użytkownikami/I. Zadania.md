1. Utwórz dwa dodatkowe konta użytkownika „tux1” i „tux2”. Nadaj tym użytkownikom hasło, aby móc się zalogować jako ci użytkownicy. Sprawdź, czy zostały utworzone konta użytkowników.

2. Przyjrzyj się różnym plikom przechowującym informacje o użytkownikach (/etc/passwd, /etc/shadow, /etc/group, /etc/gshadow), aby wyświetlić utworzone właśnie konta użytkowników. Spójrz także na katalog domowy tych nowych użytkowników, zawartość katalogu domowego i porównaj to z zawartością /etc/skel.

3. W innym oknie terminala spróbuj zalogować się jako tux1 i tux2. czy to działa?

4. Zablokuj konto użytkownika tux1.

5. W innym oknie terminala spróbuj zalogować się jako tux1. Czy możesz się teraz zalogwać?

6. Odblokuj konto użytkownika tux1.

7. Zmodyfikuj parametry starzenia się hasła dla tux1 tak, aby przy następnym logowaniu tux1 był zmuszony zresetować swoje hasło.

8. Ponownie, w innym terminalu, zaloguj się jako tux1. czy to działa? Czy poproszono Cię o zmianę hasła?

9. Utwórz dodatkową grupę „pingwiny”. Uczyń użytkowników „tux1” i „tux2” członkami tej grupy.

10. Przyjrzyj się różnym plikom przechowującym informacje o użytkownikach, aby zobaczyć, jak administrowana jest ta grupa pomocnicza.

11. Utwórz katalog grupy, /home/pingwiny. Ustaw odpowiednie uprawnienia w tym katalogu, aby użytkownicy tux1 i tux2 mogli pracować razem nad projektem w tym katalogu.

12. Przejrzyj na informacje o starzeniu się hasła dla tux1.  

13. Zobacz, ile procesów ma już twój użytkownik uruchomionych.