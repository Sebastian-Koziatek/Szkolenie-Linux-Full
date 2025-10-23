# Rozwiązania - Symlink i hardlink

## 1. W swoim katalogu domowym utwórz podkatalog „links". Przejdź do tego katalogu. Utwórz plik „abc" z dowolną treścią.

```
Kroki:
1. cd ~                              # Przejście do katalogu domowego
2. mkdir links                       # Utworzenie katalogu links
3. cd links                          # Przejście do katalogu links
4. echo "Treść pliku abc" > abc      # Utworzenie pliku z treścią

Alternatywne sposoby utworzenia pliku:
cat > abc << EOF
To jest zawartość pliku abc
Druga linia
EOF

touch abc && echo "Treść pliku" > abc

nano abc
# (wpisz treść i zapisz)

Weryfikacja:
pwd                    # Sprawdź lokalizację
ls -la                 # Lista plików
cat abc               # Zawartość pliku
```

## 2. Sprawdź informacje pliku abc. W szczególności zwróć uwagę na jego numer i-węzła, jego rozmiar i uprawnienia.

```
Szczegółowe informacje o pliku:

ls -li abc
# -i pokazuje numer i-node
# -l pokazuje szczegółowe informacje

stat abc
# Pełne informacje o pliku

file abc
# Typ pliku

Przykładowe wyjście ls -li:
1234567 -rw-r--r-- 1 user group 18 Oct 23 10:30 abc

Interpretacja:
- 1234567: numer i-node
- -rw-r--r--: uprawnienia (rw- dla właściciela, r-- dla grupy i innych)
- 1: liczba linków (hard links)
- user: właściciel
- group: grupa
- 18: rozmiar w bajtach
- Oct 23 10:30: data i czas ostatniej modyfikacji
- abc: nazwa pliku

Dodatkowe polecenia:
du -b abc             # Rozmiar w bajtach
wc -c abc             # Liczba znaków
ls -s abc             # Rozmiar w blokach
```

## 3. Utwórz dowiązanie stałe o nazwie „def" do pliku abc. Spójrz na cechy tego pliku.

```
Utworzenie hard link:
ln abc def

Sprawdzenie cech obu plików:
ls -li abc def

Porównanie:
stat abc
stat def

Obserwacje po utworzeniu hard link:
- Oba pliki mają ten sam numer i-node
- Liczba linków zwiększyła się do 2
- Oba pliki mają identyczny rozmiar
- Identyczne uprawnienia
- Ta sama data modyfikacji

Przykładowe wyjście:
1234567 -rw-r--r-- 2 user group 18 Oct 23 10:30 abc
1234567 -rw-r--r-- 2 user group 18 Oct 23 10:30 def

Ważne cechy hard links:
- Wskazują na ten sam i-node
- Modyfikacja jednego pliku wpływa na drugi
- Usunięcie jednego nie usuwa danych (dopóki link count > 0)
- Działają tylko w obrębie tego samego systemu plików
- Nie można tworzyć hard links do katalogów (zwykle)

Weryfikacja zawartości:
cat abc
cat def
# Identyczna zawartość
```

## 4. Zmodyfikuj uprawnienia pliku def (np. 400). Następnie spójrz na uprawnienia abc.

```
Zmiana uprawnień:
chmod 400 def

Sprawdzenie uprawnień obu plików:
ls -l abc def

Obserwacje:
- Uprawnienia abc również się zmieniły na 400 (r--------)
- Hard links dzielą te same metadane
- Zmiana uprawnień jednego pliku wpływa na wszystkie hard links

Wyjaśnienie uprawnień 400:
4 = read (r)
0 = no write (-)
0 = no execute (-)
Tylko właściciel może czytać plik

Testowanie dostępu:
cat abc           # Powinno działać (jesteś właścicielem)
cat def           # Również powinno działać

Przywrócenie normalnych uprawnień:
chmod 644 abc

Sprawdzenie:
ls -l abc def
# Oba pliki powinny mieć uprawnienia 644

Inne przykłady uprawnień:
chmod 755 def     # rwxr-xr-x
chmod 600 abc     # rw-------
chmod u+x def     # Dodaj execute dla właściciela
```

## 5. Spójrz na charakterystykę systemu plików i zanotuj/zapamiętaj rozmiar.

```
Sprawdzenie charakterystyki systemu plików:

df -h .
# Pokazuje wykorzystanie systemu plików dla bieżącego katalogu

df -i .
# Pokazuje wykorzystanie i-nodes

du -sh .
# Rozmiar bieżącego katalogu

stat -f .
# Szczegółowe informacje o systemie plików

Zanotuj następujące informacje:
- Całkowity rozmiar systemu plików
- Dostępne miejsce
- Wykorzystane miejsce
- Procent wykorzystania
- Liczba dostępnych i-nodes
- Typ systemu plików

Przykład:
df -h .
Filesystem      Size  Used Avail Use% Mounted on
/dev/sda1        20G  5.2G   14G  28% /

Informacje do zanotowania:
- Used: 5.2G (przed operacjami)
- Avail: 14G
- Use%: 28%

Sprawdzenie i-nodes:
df -i .
Filesystem      Inodes   IUsed   IFree IUse% Mounted on
/dev/sda1      1310720   45234 1265486    4% /
```

## 6. Usuń plik abc. Zobacz, co się stało z plikiem def.

```
Usunięcie pliku abc:
rm abc

Sprawdzenie co się stało z def:
ls -li def
cat def

Obserwacje:
- Plik def nadal istnieje i jest dostępny
- Zawartość def pozostała niezmieniona
- Liczba linków zmniejszyła się z 2 do 1
- Numer i-node pozostał ten sam

Sprawdzenie:
ls -li def
# Powinno pokazać link count = 1

Wyjaśnienie:
- Hard link nie jest "skrótem" do pliku
- To równoprawne wskazanie na i-node
- Dane są usuwane dopiero gdy link count = 0
- Usunięcie "oryginalnego" pliku nie wpływa na hard linki

Próba dostępu do abc:
ls abc
cat abc
# Powinno pokazać "No such file or directory"

Test funkcjonalności def:
echo "Nowa linia" >> def
cat def
# Plik def w pełni funkcjonalny
```

## 7. Spójrz na charakterystykę systemu plików i sprawdź rozmiar.

```
Sprawdzenie systemu plików po usunięciu abc:

df -h .
du -sh .

Porównanie z poprzednimi wartościami:
- Rozmiar wykorzystanego miejsca powinien być taki sam
- Dane nie zostały usunięte z dysku
- I-node nadal jest w użyciu (przez plik def)

Sprawdzenie i-nodes:
df -i .

Obserwacje:
- Liczba używanych i-nodes nie zmieniła się
- Dane fizycznie nadal istnieją na dysku
- System plików nie odzyskał miejsca

Wyjaśnienie:
Gdy istnieją hard linki, usunięcie jednego z plików:
- Zmniejsza link count
- NIE usuwa danych z dysku
- NIE zwalnia i-node
- NIE zwalnia miejsca na dysku

Miejsce zostanie zwolnione dopiero gdy:
- Wszystkie hard linki zostaną usunięte
- Link count osiągnie 0
- System wykona garbage collection
```

## 8. Skasuj plik def.

```
Usunięcie ostatniego hard link:
rm def

Sprawdzenie:
ls -la
# Katalog powinien być pusty (poza . i ..)

find . -name "def"
# Nie powinno znaleźć pliku

Próba dostępu:
cat def
# "No such file or directory"

Co się stało:
- Link count dla i-node osiągnął 0
- System oznaczy i-node jako wolny
- Dane będą oznaczone do usunięcia
- Miejsce na dysku zostanie zwolnione
```

## 9. Ponownie sprawdź rozmiar systemu plików.

```
Sprawdzenie po usunięciu wszystkich hard links:

df -h .
du -sh .

Porównanie z początkowymi wartościami:
- Wykorzystane miejsce powinno się zmniejszyć
- Dostępne miejsce powinno się zwiększyć
- Procent wykorzystania powinien spaść

Sprawdzenie i-nodes:
df -i .

Obserwacje:
- Liczba używanych i-nodes zmniejszyła się
- I-node został zwolniony
- Miejsce na dysku zostało odzyskane

Przykład różnicy:
Przed: Used 5.2G, Avail 14G
Po:    Used 5.2G, Avail 14G (rozmiar pliku był mały)

Weryfikacja zwolnienia miejsca:
# Utwórz większy plik do testu
dd if=/dev/zero of=duzy_plik bs=1M count=10
ln duzy_plik hard_link
ls -li duzy_plik hard_link
df -h .

rm duzy_plik
df -h .  # Miejsce nadal zajęte

rm hard_link  
df -h .  # Miejsce zwolnione

Czyszczenie:
cd ..
rmdir links  # Usuń pusty katalog

Kluczowe różnice między Hard Links a Soft Links (Symbolic Links):

Hard Links:
- Wskazują bezpośrednio na i-node
- Działają tylko w obrębie jednego systemu plików
- Nie można tworzyć do katalogów
- Nie "psują się" gdy oryginalny plik jest usunięty
- Licznik referencji w i-node

Soft Links (ln -s):
- Wskazują na ścieżkę do pliku
- Działają między systemami plików
- Można tworzyć do katalogów
- "Psują się" gdy cel zostanie usunięty
- Są oddzielnym plikiem z własnym i-node

Tworzenie soft link (dla porównania):
ln -s /path/to/target symlink_name
ls -la symlink_name  # Widać strzałkę ->
```