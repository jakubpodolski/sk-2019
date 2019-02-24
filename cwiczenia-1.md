 System operacyjny w środowisku sieciowym
=========================================

Charakterystyka systemu operacyjnego
------------------------------------

| Charakterystyka | wartość           | komentarzu |
| ------------- |:-------------:| -----:|
| nazwa      | linux |centos 7|
| program (parametry sieci)      | dunno |  |


Konfiguracja połączenia sieciowego
----------------------------------

| Parametr | wartość           | komentarz |
| ------------- |:-------------:| -----:|
| Adres IP      | 10.0.2.15 | przydzielony przez DHCP |
| Maska podsieci      | /24  | wystepuje po '/' w IP4 |
| Brama      | 10.0.2.2 | adress przez który komp łączy się z innymi kompami przerz router |
| DNS 1      | 10.10.0.8 |  |
| DNS 2      | 10.10.0.4 |  |

Schemat sieci
-------------

aby załączyć obrazek 

```markdown
![alt schemat](https://github.com/adam-p/markdown-here/raw/master/src/common/images/icon48.png)![alt schemat](https://github.com/adam-p/markdown-here/raw/master/src/common/images/icon48.png)

![alt schemat](images/my-network-schema.png)
```

nmcli -> shows available network devices
ifup 'device name' -> enables network card 
nmcli device show -> shows available network devices i more readable format
