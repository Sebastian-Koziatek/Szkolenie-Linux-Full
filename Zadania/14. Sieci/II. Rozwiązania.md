## Pakiet `ifconfig`

  

**1. Wyświetl informacje o wszystkich interfejsach sieciowych:** 

```bash
ifconfig -a
```

**2. Zadanie: Konfiguruj adres IP na interfejsie sieciowym:** 

```bash
sudo ifconfig eth0 192.168.10.100 netmask 255.255.255.0 up
```

**3. W jaki sposób wyłączysz interfejs sieciowy?**

```bash
sudo ifconfig eth0 down
```

**4. Zadanie: Wyświetl adres MAC interfejsu sieciowego:**
```bash
ifconfig eth0 | grep ether
```
---
## Pakiet `ip`


**1. Zadanie: Sprawdź informacje o interfejsach sieciowych:**
```bash
ip addr
```

**2. Zadanie: Wyświetl tablicę routingu:**
```bash
ip route
```  

**3. Konfiguracja adresu IP na interfejsie sieciowym:**
```bash
sudo ip addr add 192.168.10.100/24 dev eth0
sudo ip link set eth0 up
```

**4. W jaki sposób wyłączysz interfejs sieciowy?**
```bash
sudo ip link set eth0 down
```
  ---
## Komenda `ping`

**1. Sprawdź, czy host o adresie IP 192.168.10.1 jest dostępny w sieci lokalnej:**

```bash
ping 192.168.10.1
```

  

**2. Ustal czas odpowiedzi hosta o adresie IP 8.8.8.8 (DNS Google):**
```bash
ping 8.8.8.8
```

**3. Wykonaj ping do hosta o adresie IP 10.123.0.2, ale ogranicz liczbę wysłanych pakietów do 5:**

```bash
ping -c 5 10.123.0.2
```

**4. Wykonuj ping do hosta o adresie IP 10.123.0.2 w nieskończoność:**
```bash
ping 10.123.0.2
```

  

**5. Wykonuj ping do hosta o adresie IP 10.123.0.2 co 2 sekundy:**
```bash
ping -i 2 10.123.0.2
```

---

  ## Komenda `nslookup`

**1. Wykonaj zapytanie DNS dla nazwy domenowej "www.example.com":**
```bash
nslookup www.example.com
```

**2. Wykonaj zapytanie odwrotne DNS dla adresu IP 10.123.0.1:**
```bash
nslookup 10.123.0.1
```

  

**3. Wykonaj zapytanie DNS dla "www.example.com", korzystając z DNS Google (8.8.8.8):**

```bash
nslookup www.example.com 8.8.8.8
```

  

**4. Ustal rekord MX dla domeny "example.com":**

```bash
nslookup -query=mx example.com
```

  

**5. Wyświetl informacje o serwerze DNS dla domeny "example.com":**

```bash
nslookup -type=ns example.com
```

---

  

## Komenda `nmap`

  

**1. Wykonaj szybkie skanowanie pingowe:**
```bash
nmap -sn 10.123.0.1/24
```

  

nmap -p 80 192.168.10.2
nmap -p 1-1000 192.168.10.2

**2. Skanuj port 80 na hoście o adresie IP 10.123.0.2:**

```bash
nmap -p 80 10.123.0.2
```

**3. Skanuj porty od 1 do 1000 na hoście o adresie IP 10.123.0.2:**

```bash
nmap -p 1-1000 10.123.0.2
```

  

**4. Wyświetl informacje o wersji i usługach działających na hoście 192.168.2.50:**

  

```bash

nmap -sV 192.168.2.50

```

  

**5. Próbuj wykryć system operacyjny hosta o adresie IP 172.16.0.1:**

  

```bash

sudo nmap -O 172.16.0.1

```

  

**6. Wykonaj szybkie skanowanie otwartych portów na hoście 192.168.0.2:**

  

```bash

nmap -F 192.168.0.2

```