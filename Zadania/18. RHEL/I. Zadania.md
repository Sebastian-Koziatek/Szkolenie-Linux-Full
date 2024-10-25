  

 1. Daj swojemu użytkownikowi "szkolenie" uprawnienia do używania polecenia sudo

```bash
sudo usermod -aG wheel szkolenie

```  
2. Zaktualizuj system, użyj menagera pakietów dnf a po aktualizacji sprawdź w menagerze dnf czy jakaś aktualizacja pozostała do wykonania.

```bash
sudo dnf update -y
sudo dnf upgrade --refresh
```
3. Sprawdź jaki pakiet zawiera program który pozwoli Ci sprawdzić czy musisz wykonać restart systemu po aktualizacji i zainstaluj go
```bash
sudo dnf install -y needrestart
```
4. Sprawdź czy musisz wykonać restart systemu

```bash
needrestart
```
5. Zainstaluj pakiet mc

```bash
sudo dnf install -y mc
```
6. Sprawdź komendą man opis programu mc

```bash
man mc
```
7. Sprawdź stronę pomocy za pomocą polecenia man dla pakietu mc

```bash
man -k mc
```

  8. Sprawdź jakie serwisy są uruchomione w systemie

```bash
systemctl list-units --type=service --state=running
```


9. Sprawdź status serwisu firewall oraz ssh

```bash
systemctl status firewalld
systemctl status sshd
```

10. Sprawdź plik konfiguracyjny SSH i zobacz na jakim porcie działa twoja usługa SSH

```bash
sudo grep Port /etc/ssh/sshd_config
```

11. Sprawdź do jakich subskrypcji masz dostęp w systemie RHEL

```bash
sudo subscription-manager list --available
```