1. Wyświetl wszystkie serwisy w systemie i ich aktualny stan oraz lokalizację
```
sudo systemctl
```

2. Zainstaluj silnik stron internetowych nginx i uruchom jego deamona
```
sudo yum install nginx -y
sudo systemctl start nginx
```

3. Sprawdź czy serwis nginx'a jest uruchomiony
```
sudo systemctl status nginx   
```

4. Zastopuj działanie serwisu nginx
```
sudo systemctl stop nginx
```

5. Ponownie sprawdź czy serwis nginx'a jest uruchomiony
```
sudo systemctl status nginx   
```

6. Uruchom serwis nginx'a i sprawdź czy działa
```
sudo systemctl start nginx   
sudo systemctl status nginx   
```

7. Włącz autostart serwisu nginx w trakcie startu systemu
```
sudo systemctl enable nginx  
```

8. Sprawdź czy serwis firewalld (daemon uslugi firewall) jest włączony na twoim systemie. Jeżeli tak to wyłącz i z poziomu przeglądarki wejdź na adres IP swojego serwera.
```
sudo systemctl status firewalld
sudo systemctl stop firewalld
ip addr 
```