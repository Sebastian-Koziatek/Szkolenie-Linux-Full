1. **Czym jest YUM i jakie pełni funkcje w systemie Linux?**  
   YUM (Yellowdog Updater, Modified) to menedżer pakietów używany głównie w dystrybucjach opartych o Red Hat (np. CentOS, RHEL). Umożliwia instalowanie, aktualizowanie i usuwanie pakietów wraz z ich zależnościami, korzystając z repozytoriów online.

2. **Jakie są podstawowe różnice między YUM a APT?**  
   YUM używany jest w systemach Red Hat/CentOS, APT w systemach Debian/Ubuntu.  
   YUM korzysta z pakietów `.rpm`, APT z `.deb`.  
   Składnia poleceń i sposób zarządzania zależnościami różnią się między tymi narzędziami.

3. **Czym jest repozytorium pakietów i jaką pełni rolę?**  
   Repozytorium to zdalny (lub lokalny) katalog zawierający pakiety oprogramowania oraz ich metadane. Menedżer pakietów korzysta z repozytoriów, aby pobierać, instalować i aktualizować oprogramowanie.

4. **Jak wyświetlić listę zainstalowanych pakietów za pomocą YUM?**  
   ```
   yum list installed
   ```

5. **W jakiej sytuacji użyjesz YUM, a kiedy RPM? Podaj praktyczne przykłady.**  
   YUM: kiedy chcesz automatycznie instalować pakiety z repozytorium wraz z zależnościami.  
   RPM: kiedy masz pojedynczy plik `.rpm` i chcesz go zainstalować bez repozytorium (np. ręczna instalacja pakietu).

6. **Gdzie znajduje się plik konfiguracyjny `yum.conf`? Jakie ustawienia można w nim zmienić?**  
   Plik `yum.conf` znajduje się w `/etc/yum.conf`.  
   Można w nim ustawić m.in. lokalizacje cache, domyślne repozytoria, opcje GPG, logowanie, limity.

7. **Czy można pobierać pakiety z pominięciem weryfikacji kluczy GPG w YUM? Jeśli tak, to jak?**  
   Tak. Można ustawić `gpgcheck=0` w pliku repozytorium lub dodać opcję `--nogpgcheck` do polecenia, np.:  
   ```
   yum install --nogpgcheck pakiet
   ```

8. **Gdzie przechowywane są pliki konfiguracyjne repozytoriów dla YUM?**  
   W katalogu:  
   ```
   /etc/yum.repos.d/
   ```

9. **Jakie są kluczowe różnice między YUM a jego następcą DNF?**  
   - Lepsze zarządzanie zależnościami.  
   - Lepsza obsługa wydajności i równoległości.  
   - Obsługa transakcji rollback.  
   - DNF zastępuje YUM w nowszych systemach (np. Fedora, RHEL 8+).

10. **Czym jest „dependency hell” i w jaki sposób menedżery pakietów próbują go unikać?**  
   To sytuacja, w której różne pakiety wymagają niekompatybilnych wersji tych samych zależności.  
   Menedżery pakietów zapobiegają temu przez: rozwiązywanie zależności automatycznie, blokowanie kolizji i oferowanie wersjonowania.

11. **Na czym polega różnica między `yum update` a `yum upgrade`?**  
   W praktyce w YUM polecenia te są równoważne.  
   W DNF różnica polega na tym, że `upgrade` usuwa przestarzałe pakiety, a `update` nie.

12. **Jak wyszukać w repozytorium pakiety `wget` oraz `mc`?**  
   ```
   yum search wget  
   yum search mc
   ```

13. **Jak zainstalować pakiety `wget` oraz `mc`?**  
   ```
   sudo yum install wget mc
   ```

14. **Jak zaktualizować pojedynczy pakiet (np. `wget`) za pomocą YUM?**  
   ```
   sudo yum update wget
   ```

15. **Jak wyświetlić historię operacji wykonanych przez YUM?**  
   ```
   yum history
   ```

16. **Jak wyczyścić cache, metadane i nagłówki YUM?**  
   ```
   yum clean all
   ```
   Można też osobno: `yum clean metadata`, `yum clean headers`, `yum clean packages`.

17. **Przeanalizuj zależności wybranego pakietu (`yum deplist wget`) i spróbuj zrozumieć, co jest wymagane.**  
   ```
   yum deplist wget
   ```
   To polecenie pokaże wszystkie pakiety wymagane do działania `wget` – pozwala zrozumieć zależności systemowe.

18. **Porównaj polecenia `dnf` i `yum` dla tej samej operacji – które jest szybsze i bardziej informacyjne?**  
   DNF jest zazwyczaj szybszy, dokładniejszy w komunikatach i ma lepsze zarządzanie zależnościami.  
   Przykład porównania:  
   ```
   time yum install tree  
   time dnf install tree
   ```
