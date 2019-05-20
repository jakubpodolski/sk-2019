# firewall

  * https://access.redhat.com/documentation/en-us/red_hat_enterprise_linux/6/html/security_guide/sect-security_guide-iptables
  * https://linux.die.net/man/8/iptables

## iptables

### tabele / tables (-t)

| tabela    |  przeznaczenie   | 
| ------------- |:-------------| 
|   ``nat``    |   NAT / przekierowania          |
|   ``filter``    |  filtrowanie                 |
|   ``mangle``    |  modyfikacje, (ex. TTL       |

### łańcuchy / chains iptab
Ograniczenie tego co przychodzi
![input](input.svg)

Ograniczenie tego co wychodzi
![output](output.svg)

Ograniczenie tego co przechodzi 
![forward](forward.svg)


| łańcuch    |  przeznaczenie   | 
| ------------- |:-------------| 
|   ``INPUT``    |                               |
|   ``OUTPUT``    |                              |
|   ``FORWARD``    |                             |
|   ``PREROUTING``    |przed rozwiązaniem routingu|
|   ``POSTROUTING``    |po rozwiązaniem routingu|

### co zrobić / target (-j)

|     |  przeznaczenie   | 
| ------------- |:-------------| 
|   ``ACCEPT``    |                               |
|   ``DROP``    |jawne odrzucenie pakietu (wysłanie zwrotki)|
|   ``REJECT``    |brak odpowiedzi o odmowie (np timeout)|
|   ``LOG``    |do logu systemowego|


### Użycie

```bash
iptables -A -i <interface> -p <protocol (tcp/udp) -s <source> --dport <port> -j <target>
```
-A append
-D delete

### wykorzystanie

* Lista obecnych reguł 
  * format tabeli
  * format listy
* Czyszczenie obecnych reguł aka flush
* Domyślne zachowanie ACCEPT / DROP
* Zezwolenie na połączenie dla konkretnego portu
* NAT
  * Przekierowanie portów ip:port -> ip2:port
  * Przekierowanie portów ip:port1 -> ip2:port2

### Zadanie 


1.
   * Przygotuj konfigurację sieci gdzie ``PC0`` pełni rolę bramy NAT
   * Przygotuj konfigurację sieci gdzie ``PC1`` udostępnia usługi
   
2. * Rozbuduj konfigurację sieci dla ``PC0`` o kolejny interfejs umożliwiający komunikację z hostem ``host-only`` 
  Zabezpiecz ``PC1`` konfigurując firewall z wykorzystanie ``iptables`` tak aby zezwolicz na połącznia przychodzace
 z portem 22 (SSH) włącznie z lokalnej sieci (komputera hosta)
   * Ustaw domyślne polityki dla INPUT, OUTPUT, FORWARD kolejno, DROP, ACCEPT, ACCEPT
   * Zapisz konfigurację firewall, tak aby została odtworzona po konownym uruchomieniu maszyny
   * Zweryfikuj możliwość połączenia wykorzystując program putty (klient SSH)

3. * Skonfiguruj ``NAT`` dla PC0
   * Zweryfikuj poprawność konfiguracji dla ``PC1`` pingując dowolny adres publiczny
   * Zainstaluj serwer http ``apache`` lub ``nginx``
   * dokonaj przekierowania portów tak aby odwiedzając w przeglądarce adres w sieci ``host-only `` dla ``PC0``
     wyświetlona została strona startowa serwera zainstaloanego dla ``PC1`` 

4. * Zainstaluj program ``udp-echo-serwer`` dla ``PC1`` oraz ``udp-echo-client`` dla ``PC0``
   * skonfiguruj firewall dla ``PC1`` tak aby umożliwiał połączenia przychodzące wyłącznie dla następujacych portów
    * 80
    * 65433
   * zapewnij aby konfiguracja została załadowana po każdym uruchomieniu systemu
   * sprawdź konfigurację wykonując testowe polączenie na wskazanych wyżej portach
   * zweryfikuj brak możliwości ustanowienia połączenia na porcie 22 (SSH)


HOW TO: 
1. Dwie maszyny ( w PC0, trzy karty: Nat , Siec Nat, host only
2. PC0 (3 interfejsy up)
3. iptables -S (pokazanie firewall)  \\ iptables -P INPUT ACCEPT (zaakceptowanie wszystkich wychodzących)
Należey pamiętać, że z ssh musi być włączony (np jeżeli go zdropujemy, to nie będzie zdalnego dostępu) \\ iptables -F (default)
4. iptables -P (domyślna polityka) INPUT DROP
5. iptables (-t domyślnie) -A INPUT -i lo -j ACCEPT
6. iptables -A INPUT -p tcp --dport 22 -s 149.153.0.0/16 -j ACCEPT
7. iptables-save > /etc/iptables.up.rules (zapisanie ustawień), potem nano /etc/network/interfaces


