1. Korzystając z generatora czasu do crona, stwórz wpis który co minute będzie wysłał wiadomość do wszystkich użytkowników systemu z informacja "Crontab pozdrawia".
   
```
touch script1.sh
wall "Crontab pozdrawia"
crontab -e
*/1 * * * * /home/szkolenie/script1.sh
```
   
2. Zrestartuj serwis crona aby załadować nowe ustawienia.
```
sudo systemctl restart crond
```
   
3. Wyświetl wszystkie zaplanowane procesy crona. 
```
crontab -l
```

4. Sprawdź listę zaplanowany zadań cron dla użytkownika szkolenie
```
crontab -u szkolenie -l
```

5.  Jakimi znakami rozdzielisz poszczególne polecenia które możesz zawrzeć w cronie? 
```
; aby wykonać kolejne polecenie nie zależnie od stanu poprzedzającego polecenia
&& aby wykonać kolejne polecenie jeżeli poprzednie wykona się poprawnie
|| aby wykonać kolejne polecenie jeżeli poprzednie się nie wykona 
```

6.  Użyj polecenia aby usunąć utworzony wpis do crona (żeby nie zaśmiecał Ci systemu)
```
crontab -r
```