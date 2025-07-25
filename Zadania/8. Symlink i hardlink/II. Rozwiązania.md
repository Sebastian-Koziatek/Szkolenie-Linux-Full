1.  W swoim katalogu domowym utwórz podkatalog „links”. Przejdź do tego katalogu.
```
mkdir ~/links
cd ~/links
echo "This is abc" > abc
```

2. prawdź informacje pliku abc. W szczególności zwróć uwagę na jego numer i-węzła, jego rozmiar i uprawnienia.
```
ls -li abc
stat abc
```

3. Utwórz dowiązanie stałe o nazwie „def” do pliku abc. Spójrz na cechy tego pliku.
```
ln abc def
```

4. Zmodyfikuj uprawnienia pliku def (np. 400). Następnie spójrz na uprawnienia abc.
```
chmod 400 def
ls -li abc def
stat abc
stat def
```


5.  Spójrz na charakterystykę systemu plików i zanotuj/zapamiętaj rozmiar cs-root
```
df
df -i
```

6. Usuń plik abc. Zobacz, co się stało z plikiem def.
```
rm abc
ls -li def
stat def
cat def
```

7.  Spójrz na charakterystykę systemu plików i sprawdź rozmiar cs-root
```
 df 
 df -i
```


8.  Skasuj plik def
```
rm def
```


9.  Ponownie sprawdź rozmiar cs-root
```
df
df -i
```
