
1.  Sprawdź aktualną konfigurację sieci: nazwę hosta, adresy IP, maskę podsieci, bramę domyślną i konfiguracje DNS.  Zapisz gdzieś te dane. 
   
Nazwa hosta:
```
hostname
```

Adresy IP / Brama domyślna:
```
ip addr
```

Konfiguracja DNS:
```
cat /etc/resolv.conf
```

2.  Narzędzie ip to nowe narzędzie do sprawdzania i modyfikowania konfiguracji sieci, które jest instalowane domyślnie. Zainstaluj narzędzia ifconfig oraz route i użyj ich również do sprawdzenia konfiguracji sieci.
```
yum provides ifconfig
yum -y install net-tools
ifconfig
route -n
```

3.  Użyj nowego narzędzia dostępnego w RHEL9/CentOS9 – **nmtui** i przeprowadź konfigurację sieci używając danych zanotowanych w ptk1
```
 sudo nmtui
```

4.  Uruchom ponownie system. Sprawdź ponownie konfigurację sieci.
```
sudo reboot
``` 

5.  W jaki sposób możesz odświeżyć konfigurację sieci bez potrzeby restartowania serwera?
```
systemctl restart NetworkManager
```

6.  Dowiedz się, jaki jest adres IP [wp.pl](http://www.wp.pl/)
```
host www.wp.pl
```

7.  Zmień plik /etc/hosts. Celowo wpisz zły adres dla www.wp.pl
```
 1.1.2.5 www.wp.pl
```


8.  Wykonaj ping do www.wp.pl  jaki adres jest używany?  
```
ping www.wp.pl
```

9.  Przywróć pliki /etc/hosts poprzedniej konfiguracji.  
10. Sprawdź jakie interfejsy sieciowe posiadasz w systemie
```
ip link show
```

11.  Wykonaj polecenie ethtool na używanym interfejsie sieciowym i przeanalizuj wyświetlone dane.
```
ethtool enp0s3
```

12.  Wykonaj ping do 8.8.8.8. Spróbuj także użyć narzędzi traceroute i tracepath do tego adresu.
```
ping 8.8.8.8
traceroute 8.8.8.8
tracepath 8.8.8.8
```


13.  Za pomocą polecenia nmap zeskanuj otwarte porty na swoim adresie ip.
```
sudo nmap 192.168.10.30
```

14.  Za pomocą nmap zeskanuj całą sieć lokalną 
***!UWAGA! JEŻELI JESTEŚ W BIURZE, LUB SIECI PUBLICZNEJ LUB INNEJ SIECI KTÓREJ NIE JESTEŚ WŁAŚCICIELEM, NIE WYKONUJ TEGO PUNKTU!!!***
```
nmap 192.168.10.1-254
```

15. Za pomocą polecenia nmap określ adres IP serwera dns za pomocą którego program nmap będzie miał dokonać skanowania domeny wp.pl
```
nmap --dns-servers 8.8.8.8,8.8.4.4 wp.pl
```
