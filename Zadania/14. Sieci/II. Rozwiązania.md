***Pakiet ifconfig***

1.  Wyświetl informacje o wszystkich interfejsach sieciowych
```
 ifconfig
```

2. Zadanie: Konfiguruj adres IP na interfejsie sieciowym
```
ifconfig eth0 192.168.10.xxx netmask 255.255.255.0 up
```

3. W jaki sposób wyłaczysz interfejs sieciowy?
```
ifconfig eth1 down
```

4. Zadanie: Wyświetlaj adres MAC interfejsu sieciowego
```shell
ifconfig ens18 | grep "ether"
```

___
***Pakiet IP***

1. Zadanie: Sprawdź informacje o interfejsach sieciowych
```
 ip link show
```

2. Zadanie: Wyświetl tablicę routingu
```
ip route show
```

3. Konfiguracja adresu IP na interfejsie sieciowym
```
ip addr add 192.168.0.xxx/24 dev ens18
```

4. W jaki sposób wyłączysz interfejs sieciowy?
```bash
ip link set dev <interfejs> down
```

___
***Ping***

1. Sprawdź, czy host o adresie IP 192.168.10.1 jest dostępny w sieci lokalnej
```
ping 192.168.0.1
```

2. Ustal czas odpowiedzi hosta hosta o adresie IP 8.8.8.8 (DNS Google).
```
ping 8.8.8.8
```

3. Wykonaj ping do hosta o adresie IP 192.168.10.2, ale ogranicz liczbę wysłanych pakietów do 5.
```
ping -c 5 192.168.1.100
```

4. Wykonuj ping do hosta o adresie IP 192.168.10.2 w nieskończoność
```
ping 192.168.10.2
```

5. Wykonuj ping do hosta o adresie IP 192.168.10.2 co 2 sekundy.
```shell
ping -i 2 192.168.10.2
```
___
***nslookup***

1. Wykonaj zapytanie DNS dla nazwy domenowej "www.example.com" i wyświetl adresy IP powiązane z tą nazwą.

```
nslookup www.example.com
```

2. Wykonaj zapytanie odwrotne DNS dla adresu IP 192.168.0.1 i wyświetl odpowiadającą mu nazwę domenową (jeśli istnieje).
```
nslookup 192.168.10.1
```

3. Wykonaj zapytanie DNS dla nazwy domenowej "www.example.com", korzystając z serwera DNS o adresie IP 8.8.8.8 (Google DNS).
```
nslookup www.example.com 8.8.8.8
```

4. Ustal rekord MX dla domeny "example.com", który określa serwer poczty odpowiedzialny za tę domenę.
```
nslookup -type=mx example.com
```

5. Wyświetl informacje o serwerze DNS dla domeny "example.com", w tym adres IP serwera DNS.

```
nslookup -type=ns example.com
```
___
***nmap***

1.  Treść: Wykonaj szybkie skanowanie pingowe, aby sprawdzić dostępność hostów w sieci.
```
nmap -sn 192.168.0.0/24
```

2. Skanuj port 80 na hoście o adresie IP 192.168.10.2
```
nmap -p 80 192.168.10.2
```

3. Skanuj porty od 1 do 1000 na hoście o adresie IP 192.168.10.2
```
nmap -p 1-1000 192.168.10.2
```

3. Wyświetl informacje o wersji i usługach działających na hoście o adresie IP 192.168.2.50.
```
nmap -sV 192.168.10.2
```

4. Próbuj wykryć system operacyjny hosta o adresie IP 172.16.0.1.
```
 nmap -O 172.16.0.1
```

5. Treść: Wykonaj szybkie skanowanie, aby zidentyfikować otwarte porty na hoście o adresie IP 192.168.0.2
```
nmap -p- 192.168.0.2
```