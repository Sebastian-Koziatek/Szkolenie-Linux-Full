1.  Stwórz stały alias który po wywołaniu komendy "ping" od razu rozpocznie pingowanie adresu [wp.pl](http://wp.pl)
```
nano .bashrc
alias ping="ping wp.pl"
```
   
2.  Stwórz tymczasowy alias który spowoduje że wpisanie litery „h” wyświetli historie basha
```
alias h="history"
```  
   
3.  Wyświetl wszystkie alias które aktualnie posiadasz w systemie
```
alias
```
4.  Usuń alias "h"
```
unalias h
```
5.  *Stwórz stały alias który po wywołaniu komendy update wykona aktualizacje systemu, wyczyści cache, metadane i nagłówki menagera pakietów, wyczyści konsole oraz wypisze nam infomracje o udanej aktualizacji.
```bash
alias update="sudo yum update; sudo clean all; clear; echo 'Aktualizacja udana'"

```
