Aby rozwiązać te zadania na systemie opartym na Red Hat Enterprise Linux (RHEL) lub podobnym, jak Fedora, musimy wykonać poniższe kroki w terminalu. 

### 1. Daj swojemu użytkownikowi "szkolenie" uprawnienia do używania polecenia sudo

```sh
usermod -aG wheel szkolenie
```

### 2. Zaktualizuj system, użyj menagera pakietów dnf a po aktualizacji sprawdź w menagerze dnf czy jakaś aktualizacja pozostała do wykonania

```sh
sudo dnf update -y
sudo dnf check-update
```

### 3. Sprawdź jaki pakiet zawiera program który pozwoli Ci sprawdzić czy musisz wykonać restart systemu po aktualizacji i zainstaluj go

```sh
dnf provides */needs-restarting
sudo dnf install -y dnf-utils
```

### 4. Sprawdź czy musisz wykonać restart systemu

```sh
sudo needs-restarting -r
```

### 5. Zainstaluj pakiet mc

```sh
sudo dnf install -y mc
```

### 6. Sprawdź komendą man opis programu mc

```sh
man mc
```

### 7. Sprawdź stronę pomocy za pomocą polecenia man dla pakietu mc

```sh
man mc
```

### 8. Sprawdź jakie serwisy są uruchomione w systemie

```sh
systemctl list-units --type=service --state=running
```

### 9. Sprawdź status serwisu firewall oraz ssh

```sh
sudo systemctl status firewalld
sudo systemctl status sshd
```

### 10. Sprawdź plik konfiguracyjny SSH i zobacz na jakim porcie działa twoja usługa SSH

```sh
sudo cat /etc/ssh/sshd_config | grep Port
```

### 11. Sprawdź do jakich subskrypcji masz dostęp w systemie RHEL

```sh
sudo subscription-manager list --available
```

Wykonanie powyższych poleceń umożliwi Ci wykonanie wszystkich zadań związanych z zarządzaniem systemem i jego aktualizacją.