# I PRZYGOTOWANIE MASZYN
1. Utworzyć 3/4/5 maszyn wirtualnych
2. W VirtualBox utworzyć dwie karty sieciowe, z zadanym adresem IP, wyłączyć obsługę DHCP
3. Ustawić obłusgę kart sieciowych w ustawieniach dla każdej z maszyn wirtualnych 
4. Dla każdej z wirtualnych maszyn poleceniem ```ip addr``` sprawdzić dostępne urządzenia (karty sieciowe)
5. Dla danego użądzenia (np enp0s3) ustawić zadany adres IP poleceniem ```ip addr add``` np ```ip addr add 172.16.100.10/24 dev enp0s3```
6. Zrestować urządzenie poleceniem ```link``` np ```ip link set enp0s3 down``` ```ip link set enp0s3 up```

# II ROUTER
1. Dla każdej z maszyn upewnić się że forword'owanie jest ustawione na 1 ```cat /proc/sys/net/ipv4/ip_forward```
2. Ustawić przekierowywanie do router poleceniem ```ip route add default via 10.0.10.1 dev enp0s3``` (10.0.10.1 to router)
3. Reszta się dzieje sama XDD
4. Przetestować połączenie z PC1 z PC3 poleceniem ```ping```

# III ZAPISANIE STANU 
1. nano /etc/network/interfaces
2. dopisać ```iface enp0s3 inet static```  
           ```addres 192.168.100.1```  
           ```netmask 255.255.255.0```  
3. by się automatycznie odpalał to ```auto enp0s3```
4. tak zrobić dla każdej z kart sieciowych 
5. by działało routowanie ``up ip route add 192.168.0.0/24 via 192.168.200.2``
6. jeśli padnie to        ``down ip route del 192.168.0.0/24``              
