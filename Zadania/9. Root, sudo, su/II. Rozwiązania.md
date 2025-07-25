1. Czym się różni konto root od konta użytkownika?
```
Konto root jest domyślnym i głównym kontem administracyjnym, konto użytkownika jest stworzonym kontem które co najwyżej może posiadać uprawnienia administratora
```

2. Czym jest sudo?
```
Program używany w celu umożliwienia użytkownikom uruchomienia aplikacji, jako inny użytkownik systemu, najczęściej do wykonywania poleceń z uprawnieniami administratora.
```  
   
3. Jak z poziomu użytkownika zalogować się do konta root?
 ```
 su
```  

4. Zaloguj się do konta root i korzystając z pakietu sudo dopisz konto swojego użytkownika do listy kont uprawnionych.
```
su
visudo
```

5. Czym się rózni sudo su - od su ?

sudo su -
```
używa poświadczeni użytkownika by zalogować się na konto root, podczas logowania użytkownik będzie proszony o podanie hasła do konta użytkownika a nie konta root
```

su 
```
wywołuje logowanie do konta root używając poświadczeń przypisanych do konta root
```

6.  Przejrzyj plik konfiguracyjny sudo i utwórz dla swojego konta użytkownika wpis który pozwoli Ci wywoływać polecenia sudo bez koniecznośći podawania hasła użytkownika. 
```
sudo su -
visudo
```

Wpis:
```
użytkownik    ALL=(ALL)       NOPASSWD: ALL
```