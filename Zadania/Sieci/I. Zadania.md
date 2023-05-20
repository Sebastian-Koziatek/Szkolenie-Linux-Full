
1.  Sprawdź aktualną konfigurację sieci: nazwę hosta, adresy IP, maskę podsieci, bramę domyślną i konfiguracje DNS.  Zapisz gdzieś te dane. 
2.  Narzędzie ip to nowe narzędzie do sprawdzania i modyfikowania konfiguracji sieci, które jest instalowane domyślnie. Zainstaluj narzędzia ifconfig oraz route i użyj ich również do sprawdzenia konfiguracji sieci.
3.  Użyj nowego narzędzia dostępnego w RHEL9/CentOS9 – **nmtui** i przeprowadź konfigurację sieci używając danych zanotowanych w ptk1
4.  Uruchom ponownie system. Sprawdź ponownie konfigurację sieci.
5.  W jaki sposób możesz odświeżyć konfigurację sieci bez potrzeby restartowania serwera?
6.  Dowiedz się, jaki jest adres IP [wp.pl](http://www.wp.pl/)
7.  Zmień plik /etc/hosts. Celowo wpisz zły adres dla www.wp.pl
8.  Wykonaj ping do www.wp.pl  jaki adres jest używany?  
9.  Przywróć pliki /etc/hosts poprzedniej konfiguracji.  
10. Sprawdź jakie interfejsy sieciowe posiadasz w systemie
11.  Wykonaj polecenie ethtool na używanym interfejsie sieciowym i przeanalizuj wyświetlone dane.
12.  Wykonaj ping do 8.8.8.8. Spróbuj także użyć narzędzi traceroute i tracepath do tego adresu.
13.  Za pomocą polecenia nmap zeskanuj otwarte porty na swoim adresie ip.
14.  Za pomocą nmap zeskanuj całą sieć lokalną 
***!UWAGA! JEŻELI JESTEŚ W BIURZE, LUB SIECI PUBLICZNEJ LUB INNEJ SIECI KTÓREJ NIE JESTEŚ WŁAŚCICIELEM, NIE WYKONUJ TEGO PUNKTU!!!***
15. Za pomocą polecenia nmap określ adres IP serwera dns za pomocą którego program nmap będzie miał dokonać skanowania domeny wp.pl