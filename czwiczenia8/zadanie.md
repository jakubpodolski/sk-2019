Zadanie 1
---------

![zadanie 1](zadanie-1.svg)

1. Zaprojektuj oraz przygotuj prototyp rozwiązania z wykorzystaniem oprogramowania ``VirtualBox`` lub podobnego. 
Zaproponuj rozwiązanie spełniające poniższe wymagania:
   * Usługodawca zapewnia domunikację z siecią internet poprzez interfejs ``eth0`` ``PC0``
   * Zapewnij komunikację z siecią internet na poziomie ``LAN1`` oraz ``LAN2``
   * Dokonaj takiego podziału sieci o adresie ``172.22.128.0/17`` aby w ``LAN1`` można było zaadresować ``500`` adresów natomiast w LAN2 ``5000`` adresów    
   * Przygotuj dokumentację powyższej architektury w formie graficznej w programie ``DIA``
 


#Rozwiązanie 
##
1. W pliku ```/etc/network/interfaces``` dodać 
  PCO
   - enp0s8
		auto enp0s8
		iface enp0s8 inet static
		address 172.22.160.1
		netmask 255.255.254.0
	 - enp0s9
		auto enp0s9
		iface enp0s9 inet static
		address 172.22.128.1
		netmask 255.255.224.0
