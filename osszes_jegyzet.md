
research:


→

↓

MIKROTIK: admin #Aa123456789@
LINUXSERVER : root #Aa123456789@

putty: linuxserveradmin / #Aa123456789@

**VM Setup**
- vm-nél bepipálni hogy ssd a drive
- floppy kikapcsol
- bridged adapter on #1 card

Linux Setup
user name az cak a display name
country az uk mivel nincs magyar
 
#Aa123456789
#Bb123456789
ip/firewall/nat/add chain=dstnat disabled=no dst-port=22 protocol=tcp action=dst-nat toaddresses=172.16.0.254 to-ports=22 
22- es porton engedéllyezük, s

**firewall options**
```
ip/firewall/nat/print 
```

Újraindítás
```
system/reboot
```

bootable flag : on : innen bootol

swap-ot (page file) partot nekünk kell adni: logikai type, use as nem ext4 hanem swap area

telepítő csomag no-> kell szerver ahonnan letölti deb debian .org

proxy (internet szűrő) nincs, -> enter

grub pc: boot menu:: dev/sda ba tegye: device/sda(15,5 gb hely)
a meghajtók mappákban vannak elrendezve


nano: szövegszerkesztŐ → belépünk egy szöveg dokumebntumba (1-es kép)

research: hálózatcím
broadcast: a hálózat összes emberének megy

8.8.8.8 dns: google domain name servere (DNS)


ctrl s → elment
ctrl x → kilép a szöveges dokumentumból
minden konfig fájl: etc mappában

shutdown now: kikapcs

bridged : ip beállítása → network card internalra átrak

putty: távoli gépre csatlakozás

képernyőkép 2: "d" melletti cím beírása putty-ba

ha a putty nem megy: 
0: linux server újraindítása
1: linux serverbe belép rootal
2: nano /etc/network/interfaces
3: nincs-e elírva semmi adat
4: ctrl s, ctrl x, shutdown now
5: putty újra

linuxserveradminnak nincs jogosultsága

```
 su -
```
"jelszó"
↓
áltépés root felhasználóba
↓ 
teljes jogosultság

```
apt: application install
```

sudo egy program: le kell telepíteni

```
usermod -aG sudo linuxserveradmin
```
↓
sudo csoporthoz ezt a felhasználót tegye be



```
getent group sudo
```
↓
csoporton belül kinek van jogosultsága


```
su - linuxserveradmin
```
↓
átlépés a linuxserveradmin userba


```
sudo apt install build-essential dkms linux-headers-$(uname -r) -y
```
↓
(driver)

a linux server-be kell jelentkezni hogy a putty ban m



hullám vonal: home mappa
PARANCSOK


cat > gyumolcsok.txt   - létrehoz egy txt fájl, ezután várja contents of that file
 ctrl d vel kilépsz

mv (move) dolog mozgatása, PL.:
mv gyumlcsok.txt gyumolcsok

ls (list) dolgok listázása

research: dolgok átnevezése


grep: fájlon belüli keresés
pl:
grep -i "citrom" ~/gyumolcsok/deli_gyumolcsok.txt

↓

ha benne van, visszadja za értékesz





gzip tömörítés, za tömörít és töröl

gzip -s deli_gyumolcsok.txt.gz


research: hogyan kell egy command további funkcióját megjeleníteni:


find

sudo find / -name teszt.txt    -teszt.txt fájl keres

research: jelszó változtatás


sudo find / -name "*.txt" - kiterjesztés keresése

sudo find / -type d -name mnt    -???


sudo find / -type f (típus: fájl) -perm 644 (jogosultság 644) | more   -6 4 4 jogosultságu fájlokat kerest meg, a | more pedig hogy lapozható legyen, nem egyszerre az összeset


find / -type f ! -perm 777 | more    - 777 a legnagyobb fájl jogosultság

research: find parancs


ps: aktuális futó programok

ps -a ? minden felhasználo

ps u
ps x

ps aux | more

ez csak egy pillanatképed ad!

a top real time ban mutata


kill   - futó folyamat bezárása
kill "azonosíto"


ch mod  - jogosultság megadás (fájl, mappa)

jogok
olvas r
irás w
futtatás x (execute)t


tulajdon csoport other

7	5	1


r 4
w 2
x 1

group ig átnézni


Feladat


standby, HSRP

minden esetben interface konfigurációs módban dolgozunk;

Aktív router:
standby version 2
standby 1 "(group)" ip "virtuális ip cím"
standby 1 priority 105
standby 1 preempt   - aktív státuszt kap a router
standby 1 track "kimenő interface(pl. serial vagy gig)" -ha kimenő interface kikapcsol akkor 10-el csökkenti a prioritását -> standby router akcióba lép

Standby router:
standby version 2
standby 1 "(group)" ip "virtuális ip cím"
standby 1 preempt

Tesztelés:
ping, tracert

alapértelmezett útvonal beállítás
ip route 0.0.0.0 0.0.0.0 "kimenő interface | next hopp IP"

lebegtetett vagy tartalék alapértelmezett router
ip route 0.0.0.0 0.0.0.0 "kimenő interface | next hopp IP" Administrative distance
	AD: egy szám, nagyobb mint 1

alapértelmezett vagy tartalék útvonal beállítás
ip route NetID SUbnetMask "kimenő interface | next hopp IP" Administrative distance
	AD: egy szám, nagyobb mint 1


**SSH Setup**
```
ip domain name "domain"
crypto key generate rsa general-keys modulus 1024
ip ssh ver 2
ip ssh authentication-retries 2
ip ssh time-out 30

user admin privilege 15 secret "jelszó"
line vty 0 15
transport input ssh
login local		-helyi adatbázisból hitelesít (user admin privilege 15 secret "jelszó")
exit
copy run start
```



**DHCP Setup**
```
ip dhcp pool "POOL NÉV"		
default-router "ip cím"
dns-server "ip cím"
domain-name "domain név"
network "NetID" "subnetmask"
```
a dhcp csak akkor működik, ha van egy interface-e, kapcsolatban kell lennie a networkkel

**ipv4 setup**
```
ip dhcp excluded-address 192.168.10.1 192.168.10.9
ip dhcp excluded-address 192.168.10.254
ip dhcp pool LAN-POOL-1
network 192.168.10.0 255.255.255.0
default-router 192.168.10.1
dns-server 192.168.11.5
domain-name example.com
end
```


Kényelmi / quality of life:
```
no ip domain-lookup
do terminal history size 250
line con 0
exec-timeout 0 0
logging synchronous
```



konzol jelszó állítás után login		- nem mindenhol szükséges, de peace of mind dolog hogy mindig beírja az ember

```
service password encryption
```
*szöveg type jelszó titkosítása*





Statikus útvonal beállítás
ip route NetID SubnetMask "kimenő interface | next hopp IP"


Research: OSI rétegmodell, tracert command
icmp: ping protocol (internet command protocol)

layer 2 switchek mac cím alapján továbbítanak
layer 3 swtichek ip cím alapján is továbbítanak, sok port, hardveres továbbítási kódolás, drágább


HSRP (Hot Sandby Router Protocol) ipv4 or ipv6 ez is tud load balancingot valamilyen szinten, mind a két 
routeren van traffic (pl egy egy alhálózat) a hsrp egy cisco "találmány"
standby priotity; kinek legyen milyen prioritása: alapértelmezett érték: 100 0, 255 között mozoghat
ha a prioritás egyforma, a legnagyobb ipv4 ip címes router lép előnybe
ha preemnt ki van kapcsolva, az első router lesz a main

multicask ip cím: több helyre megy, de nem mindenkinek, az broadcast



GLBP (Gateway Load Balancing Protocol) ipv4 or ipv6
ICMP Router Discovery Protocol (IRDP)

tracert (ip cím)

standby 1: 1. csoport
ip address (ip cím megadásákor kell mask de pl standby ip-nél nem)

logging synchronous nem rontja el a parancs gépelését

FONTOS:
csak aktív routernél
int gig0/0/1
standby 1 track s0/1/0


HF: 9-es fejezet



Research: OSI rétegmodell
icmp: ping protocol (internet command protocol)

layer 2 switchek mac cím alapján továbbítanak
layer 3 swtichek ip cím alapján is továbbítanak, sok port, hardveres továbbítási kódolás, drágább


HSRP (Hot Sandby Router Protocol) ipv4 or ipv6 ez is tud load balancingot valamilyen szinten, mind a két 
routeren van traffic (pl egy egy alhálózat) a hsrp egy cisco "találmány"
standby priotity; kinek legyen milyen prioritása: alapértelmezett érték: 100 0, 255 között mozoghat
ha a prioritás egyforma, a legnagyobb ipv4 ip címes router lép előnybe
ha preemnt ki van kapcsolva, az első router lesz a main

multicask ip cím: több helyre megy, de nem mindenkinek, az broadcast



GLBP (Gateway Load Balancing Protocol) ipv4 or ipv6
ICMP Router Discovery Protocol (IRDP)

tracert (ip cím)

standby 1: 1. csoport
ip address (ip cím megadásákor kell mask de pl standby ip-nél nem)

logging synchronous nem rontja el a parancs gépelését


ipconfig 		- hálózati paraméterek


**research:** 
- csoportos címzés
- ACL
- FTP
- 

- Cisco terra term nem kell
- A packet traceres házi feladatban muszály kitölteni a nevet stb! Anélkül egyes
- A telnet nincs titkosítva; nem előnyös
- A service password encryption erősebb mint a password vagy a secret 
- dedikált ip cím vagy dedicated leased line: fix ip cím
- DHCP:Dynamic host configuration protocol
- FTP: file transfer protocol
- tracert: ping, de a packet menete folyamán echo-val meg tudjuk 
- nézni milyen routereken, eszközökön megy keresztül

#OSI_modell:, #portszámok
- 80-as port: http                  - a vpn nem a 80-as porton megy
- 443-as port: https		- titkosított http, web
- 21-es port: fttp
- 22-es port: ssh
- 23-as port:
- 25-ös port: smtp
- 53-as port: dns
- 110 pop3: email
- 20, 21: ftp
- 69-as port: tftp
- 67/68-as port: dhcp

**a dhcp 4 adatot határoz meg**
- ip
- mask
- default gateway
- dns
Optional: tartomány név



cisco 2.7.5


**switch biztonsági beállítások**
`switchport port-security`

**"tegye biztonságossa a bejelentkezést" feladat** (SSH setup / SSH beállítások)

```
hostname *hostnév*
ip domain name *test.local*


crypto key genenerate rsa general-keys modules 1024
vagy
crypto key gen rsa
*enter*
1024


*enter*
1024
ssh version 2


user *név* secret *jelszó*
vty 0 15
password *jelszó*
login local
transport input ssh
```



dolgozat: minta feladat átírva


tárgy: gyakorlas0913

host only adapter: virtuális hálózati interface - összeköti a vm-et a host géppel

iface enp0s8 ubet dhcp

mikrotik első login csak enter

a mikrotik erős hardverre jó, hálókártyának kompatibilisnek kell lennie 
mikrotik commandnál a sorrend mindegy

ha disabled=yes, kikapcsolva van. ha van egy x a ip dhcp-client/p-vel akkor ki van kapcsolva az eszköz
set,remove,add
p: listázás
set: módósítás
itt az ip címeket listázod

**két pont: visszalépés**
```
[admin@mikrotik] > ip

|
V

[admin@mikrotik] /ip > ..

|
V

[admin@mikrotik] >
```

**1-es kártya hozzáadása, bekapcsolva**
```
ip/dhcp-client/add interface=ether1 disable=no
```

**hálókártyák listázása**
```
ip dhcp-client/p
```

**A nulladik kártyát kikapcsolni (ha disabled=no akkor be van kapcsolva)**
```
ip dhcp-client/set numbers=0 disabled=yes
```


ip cím szerint listázza a kártyákat
```
ip address/p
```


**ip címet rendelünk a kettes interface-re**
```
ip address/add address=192.168.50.1/24 interface=ether2
```
*ha nem írunk maszkot, akkor az alapértelmezett érték megy át; 30*

ip címnék első vagy utolsó nem lehet


**internet megeosztás**
```
ip/firewall/nat/add out-interface=ether1 action=masquerade chain=srcnat
```
*1-es interface, action masquerade chain=*

**tűzfalon**
```
ip firewall/nat p
```




windows us time format, mivel vannak programok amivel összeakat a magyar time format

windows jelszó: Aa123456789!

VB ctr alt del: HOST del


windows network connections -> ethernet properties -> tcp/ip properties
ha nem egyből csatlakozik internethez, valami network activity megcsinálja (pl ping)


1. Mikrotik Virtualbox beállítása
   3db lan, stb
   lan1: nat
   lan2: internal network
   lan3: host only adapter
   
2. MikroTik telepítése
   Lan1: dhcp
   lan3: dhcp
   lan2: custom ip (pl 192.168.60.1/24)
   "oldja meg hogy legyen internet kapcsolat a belső hálózaton"
   
3. windows server telepítése
   windows 2022 type
   hálózat beállítása (tcp/ip)
   ping internet tesz
   internal network card


Mikrotik
**dhcp**
ip dhcp-client add interface=ether1 disable=no
ip dhcp-client add interface=ether3 disable=no
**fix ip**
ip address add address=...../24 interface=ether2
**internet megosztás**
ip firewall nat add chain=srcnat action=Masquerade out-interface=ether1
windows server


```
#dhcp
ip dhcp-client add interface=ether1 di
```
   

























**Alap konfig:**
```
hostname
enable secret
line console 0
password *jelszó*
login
line vty 0 15
password *jelszó*
login
service password encryption
copy run start
```


**Startup config törlése (erase-el visszamarad egy vlan file)**
```
delete startup-config
```



**NAT**: Network Address Destination
*Enged lanon belüli ip tartományt amit a hálózaton belüli kommunikációra lehet használni, és mégegy tartományt amit a hálózaton kívüli kommunikációra lehet használni.
Egy lan ami használ nat-ot, az egy natted network.*


chmod calculator

dns-nek két zónája van:
-reverse lookup zone  ip címhez nevet rendel

ac fő része: szervezeti egység;
wesselényi
	igazgató
	titkárság
	tanuló
		11
			j
				diák


ikt feladat:
3 fős csoportok
cég kitalálása
	szervezet kialak.
	szerver
	pl iskola departmentek
	csoportok
	webszerver
	css html alap



dchp-t adunk
```
ip/dhcp-client/add disabled=no interface=ether1
```


**Linux alapparancsok**

**"cmd" törlése**
```
clear
```


**ki van bejelentkezve, mióta**
```
who
```


**Több információ ad adott parancsról**
```
man
```
pl.:
```
man clear
```
|
V
több információ a "clear" parancsról


Bejelentkezési jelszó változtatása
```
passwd
```

pl.:
```
passwd linuxserveradmin
```
|
V
*régi és új jelszó megadása*
|
V
*jelszó megváltztatva*


**szövegszerkesztő program**
```
nano
```


**realtime futó programok**
```
top
```



**VLAN**

***Quality of life dolgokat beállítani!***


**Szórásos kommunikációk:** 
- ARP (Address Resolution Protocol),
- DHCP ("kitől kell ip cím?")

itt mindig 2960-as ról van szó
**VLAN típusok:**
 - default, (1-es): összes port, virtual interface vlan aminek van ip címe
 - native (1-es): fővonalon, több vlan infóját szeretnénk nézni; cimkézetlen kereteket kezel
 - management vlan: 1 by default, nem lehet törölni, átnevezni, megtekintése show vlan brief |  felügyeleti vlan, eszközök managelt, végeszköz ne tartozzon hozzá
 - adat vlan: felhasználóknak, mehet 1-től 1000 g, 1200-1500: special; fentartott vlan
 - voip vlan (voice over ip): switchen egy interface>ip>ezen keresztül megy a voice

címke:
- típus
- prioritás 3 byte
- CFI (canonical format identifier) 1bit
- VID 12bit, 4096 vlan


**hang vlan (voip) ellenőrzés:**
```
show interfaces fa0/18 switchport
```

VLAN tartományok catalyst kacspolókon
```
show vlan brief
```
*vlan1 - 1000-1200 vlan lefoglalt, automatikusan létrejön*
vlan konfiguráció flash memory-ban van tárolva, nem kell menteni

kiterjesztett vlanok: 1006- 4096: ügyfélkiszolgálás, kevesebb vlan fucntion, nagyvállalatokban hasznos futó konfigban van,

**vlan létrehozási parancsok**

**global config**
```
configure terminal
```

**create vlan with valid id number**
```
vlan *vlan id*
```






**set port to access mode**
```
switchport mode access
```

**interface config**
```
interface *interface id*
```

**assign the port to a vlan**
```
swithcport access vlan *vlan id*
```

**back to priv. exess mode**
```
end
```

|
V
ez a port bekerül a 20-as vlan-ba



***Hang vlan***
mindkét eszköznek támogatnia kell
1 adat vlan(20), 



**VOIP setup**
```
vlan 20
name student
vlan 150
name VOICE
exit
interface fa0/18
swithport mode access
swithcport access vlan 20
mls qos trust cos                 -quality of service   constant device cisco phone?? - ez a szolgáltatás alapján megy a voice vlan
switchport voice vlan 150
end
```
"a QoS megvalósítása meghaladja ennek a tanfolyamnak a kereteit."



vlan summary, összegzés
```
show vlan summary
```


hozzáférés tagok megváltoztatása

eltűnik egy port: hozzárendelted egy vlan hoz > kitörölted a vlant> no port



vlan törtlése
```
no vlan
```

or

```
delete flash:vlan.dat
```
**HA NINCS JÓL BEÍRVA TÖRLI AZ EGÉSZ FLASH-T!!

or

```
delete vlan.dat
```


alaphelyzet:
```
erase startup config
delete vlan.dat
restart
```

no mentés, resetelni akarom



rövid brief
```
show vlan brief
```


research: unicast mac address



vlan átnevezés
```
vlan 10
name *name*
```
**Natív és a management vlan ne legyen egy vlanon!**


VLAN-nak név adás
```
do terminal history size 250
vlan 10
name Faculty/Staff
vlan 20
name Students
vlan 30
name Guest(Default)
vlan 99
name Management&Native
vlan 150
name VOICE
```

history
```
do show history
```



```
S2(config)#int fa0/6

S2(config-if)#switchport mode access

S2(config-if)#switchport access vlan 10

javítás
S2(config-if)#switchport access vlan 30
```



**portok adatai**
```
do show ip interface brief
```






**trunk módok:**
- trunk
- non trunk(access mode)
- dynamic mode(auto, desireable)






do terminal history size 250

vlan 10

name Admin

vlan 20

name Accounts

vlan 30

name HR

vlan 40

name Voice

vlan 99

name Management

vlan 100

name Native

do show history

tartomány 



processor
memory
motherboard
laptop
cable
pin
header
connector
charger
keyboard
mouse
microphone
bluetooth
internet
router
switch
hub
universal serial bus (usb)
virtual
computer
graphics card
battery
fan
heatsink
adapter
read only memory(rom)
vpn: virtual private network
power supply
ssd: solid state drive
motherboard
hdd: hard disk drive
FDD: Floppy Disk drive
notebook
power cable
scanner
webcam



az ssh csak egyedi nevet fogad el

**OSI modell**
7: alkalmazás réteg
6: prezentáció réteg (pl. jpg, gif stb)
5: viszonylati (session) réteg
4: szállítása(2. (egfontosabb:) 2. port: forrás(véletlen) , 10 port ami megmondja hogy a túloldalon ki yúljon hozzá( 80)
3: hálózatiréteg; forrás ip, cél ip
2: adatkapcsolati réteg - kereteket küldözget
1: bitek: hardver, physical

**tcp/ip modell:**
megkapta-e
létezik-e még a másik
következő röp.:

fizikai, logakai topológia
hogy kapcsolunk az internethez
probléma:
elfogytak a ipv4 címet
solution: 10.0.0.8 172.16.0.0/12
otthoni 192.168.0.0/24                                  - alhálózatokban /24
portszám > ip cím                                         -natolásnak hívjuk (címfordítás)

ip
maszk
default gateway
dns

switchen keresztül mac címmel kommunikálunk

RIP 2
OSPF
ACL lista(portszám alapján)


**intranet**: company only
**extrane**t: suppliers, customers, collaborators
**Internet**: the world



tp/ip: három lépéses kézfogás


UDP: videókommunikációra használt | hibatűrés valamilyen szinten felesleges, pár pixel elveszik az nem baj, sávszélesség kell hozzá

hibrid felhő: egyik része publikus, másik privát, csak groupoknak elérhető


utolsó iő cím: broadcast

prefixum: a hálózat hány biten van | hány bithez ne szabad hozzányúlnom mivel az másik hálózatban lenne

jobb: hálózatok száma

ln:legnagyobb hálózat/network


dolgozat: október 4


research: trello

MikroTik: admin/admin or Aa


linuxserverdc: root/#Aa123456789@
putty: linuxserverdcadmin / #Bb123456789 @
putty su -: #Aa123456789 @

windows_client: winadmin/#Aa123456789@

windows_client telepítés:
keyboard layout: HU, első kettő stock


fájlkezelő> this pc properties > advanced system settings> computer name> descrip:winclient > change> comp name win client> domain> xycompany> enter> felh. admininstrator> aa jelszó> restart

restart után
other user xycompany\Administrator >linux admin jelszó (Aa)

reverse lookup zone> zone wizard> primary

jelszavak: asd123!
johnson william must change pw
personelnek nem kell pw change



Webszerver telepítése(linux server)
```
apt install apache2 -y
```

windows client tartomány adminnal belépni
administrative tools megnyitása> control panel> system ???> dns > 172.16.0.254> forward lookup zones > xy company> new host> name:www, domain name> www.xycompany.xy. , ip address> 172.16.0.254> add host>done> www host kész

böngésző> http://www.xycompany.xy//  (apache kezdőoldala)

linuxserver: itt tároljuk a szervert: 
```
cd /var/www/html/
```

```
ls
```

```
rm index.html
```


index fájl létrehozása
```
nano index.html
```
V
példa weboldal
```
<center><h1>Welcome to the XYCOMPANY website!</h1></center>
```

*crtl s, ctrl x*

V

weboldal frissítése




vlanok közötti forgalom irányítás

3 féle:
- hagyományos: minden vlan-nak van interface-e


általános subinterface
```
interface inerface_id.subinterface_id
```
a subinterfaceke beállítása:

```
encapsulation dot1q *vlan id* [native]
```

```
ip address *ip address* *mask*
```
nem kell felkapcsolni!
ha megvagyunk, kilépünk és felkapcsoljuk a alinterfaceket(mindegy milyen sorrend ha qof van)

**Alinterface config**
```
interface G0/0/1.10
description Default Gateway for VLAN 10
encapsulation dot1Q 10
ip add 192.168.10.1 255.255.255.0
```

dot1q: szabvány


hostname R1
no ip domain-lookup
enable secret class
line console 0
password cisco
login
line vty 0 4
password cisco
login
service password-encryption
banner motd "Authorized Users Only!"


copy running-config startup-config
clock set 15:46:00 22 September 2023

```
vlan 3
name Management
vlan 4
name Operations
vlan 7
name ParkingLot
vlan 8
name Native
```



interface vlan 3
ip address 192.168.3.12 255.255.255.0
no shut
exit
ip default-gateway 192.168.3.1




vlan ellenőrzése
```
show vlan brief
```


trunk ellerőrzés
```
show interfaces trunk
```

native vlan: 1-es

**hozzáférési vlan problémák**
megfelelő vlan (nem lekapcsolt stb)
trunk módba konfiguráltuk, nem access
rossz alhálózat, rossz ip tartomány

**router problémák**
alinterface rossz ip cím

alinterface rossz encapsulation > other vlan
V
```
show interfaces

*or*

running config
```


vlan kitöröl> port is elveszik

minden pc nél a szerver ip a dns



**szórás mac cím:**
FF:FF:FF:FF:FF:FF 

**DHCPOFFER**
- én mac cím, hozzátartózó ip
- default gateway
- DNS szerver


dhcp szórásból kizárás
```
ip dhcp excluded-address *ip vagy ip tartomány*
```


pool nevezés / medence nevezés
```
ip dhcp pool *pool név*
```


hálózat cím: amikor a gépek bitjei nullások, kell hogy tudjam milyen hálózatban vagyok, alongside mask

define the address pool
```
network **
```


dhcpv4 example /példa (cisco fejezet 10: 10.1.2.1 "A DHCPv4-szerver alapbeállításainak megadása")
```
ip dhcp excluded-address 192.169.10.1 192.168.10.9
ip dhcp excluded-address 192.169.10.254
ip dhcp pool LAN-POOL-1
network 192.168.10.0 255.255.255.0
default router 192.168.11.5
dns-server 192.168.11.5
domain-name example.com
end
```


|: szűrés

```
show running-config | section dhcp
```


interface 
ip helper address

67/68 portszám: dhcp



**vlan tulajdonságok**
*automatikusan létrejön
minden port hozzá van rendelve
alapértelmezett manager vlan (vty 1 15 hozzá mey)
no törlés/átnevezés*


**trunk konfig**
```
swithcport mode trunk
switchport trunk native
switchport trunk allowed
```

DTP: Dynamic Trunking Protocol
NIC: Network Interface Card
CLI: Command Line Interface


mire van a vlan:


tagelés

82 szabvány: hálózat 
.11: wifi

unicast frame: 1 konkrét mac cím


a trunk 4 bit az a dot1q szabvány



packet tracer (házi parancsok (not done))

**SW1**
```
hostname SW1
enable secret class
line vty 0 15
password cisco
login
line con 0
password cisco
login
exit
service password-encryption
banner motd "Authorized personel only!"
no ip domain-lookup
do copy run start
```

```
vlan 20
name Management
interface vlan 20
ip address 192.168.20.1 255.255.255.254
exit
ip default-gateway 192.168.20.254
```
SW2-él az ip .2 nem .1, SW3-nál pedig .3


**pc(cili) desktop> ip configuration**
ipv4: 192.168.24.10
mask: 255.255.255.0
def. gateway: 192.169.23.1 (első kiosztható)
dns: 192.168.100.10


**Switchekbe**
```
vlan 22
name LAN_A
interface vlan 22
exit
interface f0/1-7
no shut
switchport mode access
switchport access vlan 22
no shut
exit 
```

```
vlan 23
name LAN_B
interface vlan 23
exit
interface f0/8-14
switchport mode access
switchport access vlan 23
no shut
exit 
```

```
vlan 24
name LAN_
interface vlan 24
exit
interface f0/15-18
switchport mode access
switchport access vlan 24
no shut
exit 
```


```
vlan 999
name Native
vlan 1000
name BlackHole
```



**SW1:**
```
int g0/1
switchport mode trunk
switchport trunk native vlan 999
switchport trunk allowed vlan 20,22,23,24,999,1000
no shut
```

```
int g0/2
switchport mode trunk
switchport trunk native vlan 999
switchport trunk allowed vlan 20,22,23,24,999,1000
no shut
```




**ROUTER**
```
hostname R1
enable secret class
line vty 0 15
password cisco
login
line con 0
password cisco
login
exit
service password-encryption
banner motd "Authorized personel only!"
no ip domain-lookup
do copy run start
```


```
int gig0/0/1.20
encapsulation dot1Q 20
ip address 192.168.20.254 255.255.255.0
no shut

```


```
int gig0/0/1.22
encapsulation dot1Q 22
ip address 192.168.22.1 255.255.255.0
no shut

```


```
int gig0/0/1.23
encapsulation dot1Q 23
ip address 192.168.23.1 255.255.255.0
no shut

```


```
int gig0/0/1.24
encapsulation dot1Q 24
ip address 192.168.23.1 255.255.255.0
no shut

```

```
int gig0/0/1.
encapsulation dot1Q 23
ip address 192.168.23.1 255.255.255.0
no shut

```


**MikroTIk setup**
- Név: MikroTik_router
- RAM: 128MB
- CPU: 1
- SSD: 2GB
- OS: Other/Unknown(64-bit)
- Network:
	- Adapter 1: NAT
	- Adapter 2: Internal
	- Adapter 3: Host- only
- LAN: 192.168.9.1/24



mikrotik commandok:
```
ip/dhcp-client/add interface=ether1 disabled=no

ip/dhcp-client/add interface=ether3 disabled=no

ip address/add interface=ether2 address=192.168.5.1/24

ip firewall/nat add chain=srcnat out-interface=ether1 action=masquerade

ip firewall/nat add chain=dstnat in-interface=ether3 action=dst-nat dst-port=50000 to-adresses=192.168.5.2 to-ports=3389 protocol=tcp

```


webszerver (ha kell)

```
ip firewall/nat add chain=dstnat in-interface=ether3 action=dst-nat dst-port=80 to-addresses=192.168.5.2 protocol=tcp
```


**win22coreGG (non GUI)**
- Név: win2022srvgg
- network: internal
- RAM: 2gb
- CPU: 2
- IP 192.168.9.2/24


- távoli elérés
- "oldja meg hogy legyen internet a windows serveren!" (ping working)
- webszerver, weboldal


time and currency format: magyar

jelszó: #Aa12346789!
**windows webserver**
```
Install-windowsfeature AD-domain-services -includeManagementTools
```

```
install-windowsfeature web-server -IncludeManagementTools
```




wincore html 
```
cd \

cd .\inetpub\wwwroot\

notepad index.html
```
*a notepad úgy funkcionál mint a nano*

V
ip cím egy böngészőbe (itt 192.168.56.105)

meta charset ="utf8"


feladat: mikrotik, win core servre(ip, internet van), win core program telepítése

mikrotik oldalt dob be> rossz port, nincs

ip firewall/nat remove
V
2

tartományba léptetés
this pc> properties> system properties> *pc name change*> "win10client"


192.168.4.1






**TEST WEBSITE**
**TEST WEBOLDAL**
**TEST HTML**
```
<HTML>

<HEAD>

<TITLE>Your Title Here</TITLE>

</HEAD>

<BODY BGCOLOR="FFFFFF">

<CENTER><IMG SRC="clouds.jpg" ALIGN="BOTTOM"> </CENTER>

<HR>

<a href="http://somegreatsite.com">Link Name</a>

is a link to another nifty site

<H1>This is a Header</H1>

<H2>This is a Medium Header</H2>

Send me mail at <a href="mailto:support@yourcompany.com">

support@yourcompany.com</a>.

<P> This is a new paragraph!

<P> <B>This is a new paragraph!</B>

<BR> <B><I>This is a new sentence without a paragraph break, in bold italics.</I></B>

<HR>

</BODY>

</HTML>
```


- [x] Ki mit csinál


virtualbox előbb, aztán packet tracer





**Tasks:**
- [ ] packet tracer
- [ ] virtualbox
- [ ] ppt (kész termék)
- [ ] dokumentáció (word)
- [x] logó
- [ ] html



**Gergő**
- Dokumentáció
	- részletes
- PPT (kész termék)
	- mivel foglalkozik a cég
- VB


**Közös V/G**
- HTML


**Viktor**
- logó - done
- Packet tracer
- ár lista (copy/paste)
- parancsok PT: mitcsinálnak (nem konkrétan a parancsok)
- 


**Kristóf**





- mindegyik kliens windows-t futtat
- A hálózatot vlan-okra kell bontani, vlan-ok közötti forgalomiránítás
- A Switchek, routerek, kábelezés tervezése és kivitelezése
- 


**PACKET TRACER**

- milyen eszközök, milyen kábelek


- 1 SOHO router - wifi kapcsolat

**20 gép**, **ebből***
- 2 vezetőség
- 2 pénzügy
- 1 rendelés átadása
- 15 három egységben elosztva / renelések feldolgozása



**Iroda**
- 1 szerver - tartomány vezérlő, címtár szolgáltatásban tárolja a felhasználókat, weboldalt tárolja (lehet linux vagy windows)
- 



**HTML**

- weboldal rövid bemutatásról, szolgáltatás (pl vásárlás), cég elérhetőségei








--------------------start--------------------

winclient jelszó
minden más: #Aa23456789!

winclient security questions: mindegyiknél első / a


router ip: 192.168.10.1
server ip: 192.168.10.254




**ack:** acknowledgement
**fe08::1** : első hálózat privát
**Host:** Házigazda, végponti eszköz
**Node:** switch vagy router
**LLA:** Link Local Address
**GUA:** (global unicast address)
**link local address default FE80::1 : ** - minden kliens innen megy ki


Új ip cím
```
ipconfig /renew
```

DHCP letilás
```
no servie dhcp
service dhcp
```

MTU: Maximum transfer Unit: 1500


állapotmentes ip cím: a végét én generálom, mivel az nincs előre legenerálva dhcp kiszolgáló adja meg


FLAG:
```
ipv6 md managed-config

ipv6 nd other-config-flag
```

**ff0:** csoport ip címzés

**EUI-65:** (Extended Unique Identifier) (FFe)
ipv4 címzés bitek:N, H, n, h: network device, host bitek


router
**cisco 8.2.7**
1. The SLAAC process uses RA messages and can also respond to RS messages from a host.
2. The **ipv6 unicast-routing global config** command is required for a router to join the IPv6 all-routers group.
3. SLAAC sets the flags to A=1. M=0, O=0.
4. A host sends a Router Solicitation (RS) message to the IPv6 all-routers group to locate an online router.
5. A host uses DAD to ensure an IPv6 address is unique on the local network.


```
ipv6 unicast-routing

ipv6 dhcp pool IPV6-STATELESS

dns-server 2001:db8:acad:1::254
domain-name example.com
exit

int Gigt0/0/1

```


Ip alapján mac címek (windows cmd)
```
arp -a 
```

destination helper - 
```
interface gigabitethernet 0/0/1
ipv6 dhcp relay destination *mac cím* *interface*
exit
```



```
hostname S2
no ip domain-lookup
enable secret class
line con 0
password cisco
login

line vty 0 4
password cisco
login

service password-encryption
banner motd "Authorized Users Only!"

```

S2
```
interface range f0/1-4, f0/7-17, f0/19-24, g0/1-2
shutdown
end

copy run start
```



router 2
```
hostname R2
no ip domain lookup
enable secret class

line con 0
password cisco
login

line vty 0 4
password cisco
login


service password-encryption
banner motd "Authorized Users Only!"

ipv6 unicast-routing

exit
copy running-config startup-config



conf t


interface g0/1
ipv6 address fe80::1 link-local
ipv6 address 2001:db8:acad:3::1/64
no shutdown
interface g0/0
ipv6 address fe80::2 link-local
ipv6 address 2001:db8:acad:2::2/64
no shutdown

ipv6 route ::/0 2001:db8:acad:2::1

end
copy running-config startup-config
```


R1
```
ipv6 dhcp pool R1-STATELESS
dns-server 2001:db8:acad::254
domain-name STATELESS.com
interface g0/1
ipv6 nd other-config-flag
ipv6 dhcp server R1-STATELESS


ipv6 dhcp pool R2-STATEFUL
address prefix 2001:db8:acad:3:aaa::/80
dns-server 2001:db8:acad::254
domain-name STATEFUL.com


interface g0/0
ipv6 dhcp server R2-STATEFUL
```



R2
```
interface g0/1
ipv6 nd managed-config-flag
ipv6 dhcp relay destination 2001:db8:acad:2::1 g0/0
```


1. legnagyobb (4000)
2. hatvány kitevő

**ipv6 címzés**
- 4 biten 0-tól f-ig
- 0DB8
- 2 :: közötte akárhány 1-es lehet



1. név változatatás
2. hálózat beállítása
3. remote desktop
4. idő beállítása
5. tesztelés (remote desktop)
6. ezután teszünk fel szolgáltatásokat


windows/mikrotik jelszó: #Aa12346789 !

windows server UI > powershell (run as administrator)
```
sconfig
```
V
windows server core ui, itt pl. könnyebben be lehet állítani a remote desktopot


gns3 - packet tracer alternative virtual boxxal





windows server network: Internal
winclient network: internal




server ip: 192.168.11.2
router ip: 192.168.11.1
GROUP1, vlan 10 pool: 192.168.11.11 192.168.11.19
GROUP2, vlan 20 pool: 192.168.11.21 192.168.11.29
GROUP3, vlan 30 pool: 192.168.11.31 192.168.11.39



ipv6 enable (router)
```
ipv6 unicast-routing
```

```
description Link to Admin LAN
```


```
hostname S-21

no ip domain-lookup

dp terminal history size 250

line con 0

logging synchronous

exec-timeout 0 0


ipv6 unicast-routing

in gig0/0/0

description Link to Admin LAN

ip address 192.168.101.1 255.255.255.0

ipv6 address 2001:db8:1006:101::1/64

ipv6 address fe80::1 link-local

no shut


int gig0/0/1.101

des Management LAN

encapsulation dot1q 101

ip address 192.168.101.1 255.255.255.0



int gig0/0/1.102

description Link to LAN-A

encapsulation dot1q 102

ip address 192.168.102.1 255.255.255.0

ip helper-address 192.168.100.10

int gig0/0/1.103

description Link to LAN-B

encapsulation dot1q 103

ip address 192.168.103.1 255.255.255.0


int gig0/0/1.999

encapsulation dot1q 999 Native


int gig0/0/1

des Trunk to S-11

no shut


int gig0/0/2.101

description Link to Management LAN

encapsulation DOt1q 101

ipv6 address 2001:db8:1006:101::1/64

ipv6 address fe80::1

ipv6 address fe80::1 link-local


int gig0/0/2.102

description Link to LAN-C

encapsulation dot1Q 102

ipv6 address 2001:db8:1006:102::1/64

ipv6 address fe80::1 link-local


encapsulation dot1Q 103

int gig0/0/2.103

description Link to LAN-D

encapsulation dot1Q 103

ipv6 address 2001:db8:1006:103::1/64

ipv6 address fe80::1 link-local

encapsulation dot1Q 999 Native


int gig0/0/2

des trunk to S-21

no shut

ipv6 dhcp pool LAN-C

dns-server 2001:db8:1006:101:10

domain-name alma-6.pt

int gig0/0/2.102

ipv6 nd other-config-flag

ipv6 dhcp pool LAN-D

address prefix 2001:db8:1006:103::/64

dns-server 2001:db8:1006.103::10

dns-server 2001:db8:1006:100::10

int gig0/0/2.103

ipv6 nd managed-config-flag

ip dhcp excluded-address 192.168.103.1 192.168.103.24

ip dhcp excluded-address 192.168.103.76 192.168.103.254

ip dhcp pool LAN-B

default-router 192.168.103.1

dns-server 192.168.100.10

domain-name alma.pt

network 192.168.103.0 255.255.255.0

do copy run start
```



S-11

```
S-11(config)#do show history

hostname S-12

no ip domain-lookup

do terminal history size 250

line con 0

logging synchronous

exec-timeout 0 0

exit

vlan 101

name Management

vlan 102

name LAN-A

vLAN 103

name LAN-B

vlan 999

name Native

vlan 1000

name Blackhole

exit

int range fa0/1-9

switchport mode access

switchport access vlan 102

exit

int range fa0/10-19

switchport mode access

switchport access vlan 103

exit

int range fa0/20-24

switchport mode access

switchport access vlan 1000

sh

exit

int range gig0/1-2

switchport mode trunk

switchport trunk native vlan 999

switchport trunk allowed vlan 101-103

exit

int vlan 101

description Management interface

ip address 192.168.101.12 255.255.255.0

no shut

exit

ip default-gateway 192.168.101.1

do copy run start

do show history
```

```
ipv6 nd ra dns server 2001:sb8?1006:100::10
```


Az IPV6-nak 3 féle dhcp-je van:

- SLAAC Only - stateless
```
ipv6 unicast routing
```


- SLAAC with DHCP Server (stateless DHCPv6)


- DHCPv6 Server (Stateful DHCPv6) stateful: állapottartó


ipv6 DHCP konfig
```
ipv6 address fe80::1 link-local
ipv6 nd ra dns server 2001:DB9:1006:100:10
ipv6 address 2001:DB9:1006:100:10/64
ipv6 nd other-config-flag
ipv6 dhcp server LAN-C
```


doga:
- kell encapsulation dot1q
- alap konfig
- vlan létrehozáda, hozzárendelés
- trunk / Dynamic Net Protocol (DTP) (dynamic trunk, lehet trunk és non trunk (access))
	- 2 állapot:
		- trunk only
		- Ne egyeztessen:
```
		switchport nonegoitate
```





1.:jelszavak/autenctication
- line con 0 login/ ssh: login local: helyi hitelesítés
- távoli hitelesítés: külső szerveren van a jelszó (TACACS+)





**vizsga feladat:**
2 router sorossal öszekötni: /30-as hálózat: 30 bit foglalt, 2 van szabadon (+ hálózat és szórás), nincs hely + címnek, mivel a két router foglalja a 2 kiosztható ip címet


**melyik mac cím melyik ip címhez tartozik**
```
show ip dhcp binding
```

**relay agent:** továbbítási szolgáltatást nyújt


dhcpv6 lépések:
1. solicit
2. advertise
3. request
4. reply
5. 

- feldarabolja a fájlt
- azonosítja a fájlt és darabszámot ad neki (hanyadik segment)
- ellátja portszámmal



```
access-list 1 permit 0.0.0.0 255.255.255.255
access-list 1 permit any
```
*A két parancs ugyan az*


ACL Létehozása
- használjuk belső és külcső hálózat között
- beérkező és kimenő forgalom szabályzására alkalmas
- a saját hálózatunk határ forgalomirányitó interface-én használjuk


Fordítás
Bal oldal:
- Alapozd az ACL-eket a biztonsági eljárások szerint
- Készíts egy leírást, mit csináljonaz ACL
- Használj egy szövegszerkesztőt hogy létrehozz, módosíts, és elmentsd az ACL-t
- Teszteld az ACL-T egy fejlesztői felületen mielőtt beépíted egy valódi hálózatba

Jobb oldal:
- Ez biztosítja, hogy betartsa a szervezeti biztonsági irányelveket.
- Ez segít elkerülni a véletlenül kialakuló potenciális hozzáférési problémákat.
- Ez segít létrehozni egy újra felhasználható ACL-könyvtárat.
- Ez segít elkerülni költséges hibákat.

délután 2- negyed 3 közöt és nyolcig




webszerver directory nem mindig van ott,
külső gép: host
-windowsfeature *webserver* -includemanagementtools


**Windows core beállítások**

domain létrehozása
```
Install-ADDSFOREST -DomainName sulika.gg -DomainNetbiosName sulika -Force -DomainMode  7 -ForestMode 7 -InstallDns -NoRebootOnCompletion
```
*Miután a domain be van állítva, a távoli elérésbe domainnel kell belépni (itt sulika\Administrator) - ugyan az a jelszó*


firewall kikapcsolása / tűzfal kikapcsolása
```
netsh advfirewall set allprofiles state off
```


**Tartomány**
```
Install-WindowsFeature AD-Domain-Services -IncludeManagementTools

Install-ADDSFOREST -DomainName sulika.gg -DomainNetbiosName sulika -Force -DomainMode  7 -ForestMode 7 -InstallDns
```

**DHCP**
```
Install-WindowsFeature DHCP -IncludeManagementTools


add-DHCPServerV4Scope -name "scop1" -startrange 192.168.5.100 -endrange 192.168.5.121 -subnetmask 255.255.255.0

Set-DHCPServerV4OptionValue -dnsdomain sulika.local -dnsserver 192.168.5.2 -router 192.168.5.1

Add-DHCPServerInDC -dnsname win2022SRVcore1011GG.sulika.gg
```


Feature-ek / package-ek listázása
```
get -WindowsFeature
```

```
get -dhcpserverV4scope
```


remove scope (dhcp)
```
get-dhcpserverv4scope

remove-dhcpserverv4scope -scopeid *ip cím, scope id*
```


gép neve
```
hostname
```

mikrotik core tartomány win 10 


dolgozat:
telepítés:
	- windows core
	- windows server (GUI)
Dokumentálni kell mindent! erre járnak a pontok


szerda ne reggel
csütörtök reggel






**windows core / powershell**
**reboot**
```
shutdown /r t 0
```

**shutdown**
```
shutdown /s t 0
```


**server hozzáadása:**
jobb fent manage>add servers

**server törlése:**
	jobb fent manage>remove roles and features



külön web és fájlszerver és noymtató (linuxon, https)



**packet tracer router konfig**
```
R1(config)# do show history

no ip domain-lookup

do terminal history size 250

line con 0

exec-timeout 0 0

logging synchronous

hostname R1

line con 0

password Alma1234!

login

exit

emable secret Barack1234!

enable secret Barack1234!

line vty 0 4

password Citrom1234!

login

logging synchronous

exec-timeout 5 0

exit

service password-encryption

banner motd "Authorized personel only!"

ip domain-name gyak.pt

crypto key generate rsa general-keys

ssh ver 2

ip ssh authentication-retries 2

ip ssh time-out 15

ssh ver 2

line vty 0 4

login local

transport input ssh

exit

do copy run start

int gig0/0/1

exit

int gig0/0/1.100

encapsulation dot1Q 100

description Link to Management LAN

ip addres 192.168.100.6 255.255.255.248

exit

int gig0/0/1.101

encapsulation dot1Q 101

description Link to Server LAN

ip address 192.168.101.14 255.255.255.240

exit

int gig0/0/1.102

description Link to LAN-A

ENcapsulation DOt1Q 102

ip address 192.168.102.1 255.255.255.128

int gig0/0/1.103

description Link to LAN-B

ENcapsulation DOt1Q 103

ip address 192.168.103.1 255.255.255.192

exit

int gig0/0/1.999

ENcapsulation DOt1Q 999 Native

exit

int gif0/0/1

int gig0/0/1

description Trunk to S1

no shut

exit

ip dhcp excluded-address 192.168.102.1 192.168.102.15

ip dhcp excluded-address 192.168.103.1 192.168.103.15

ip dhcp pool LAN-A

default-router 192.168.102.1

dns-server 192.168.101.10

domain-name gyak.pt

network 192.168.102.0 255.255.255.128

exit

ip dhcp pool LAN-B

default-router 192.168.103.1

dns-server 192.168.101.10

domain-name gyak.pt

network 192.168.103.0 255.255.255.192

exit

do copy run start

do show history
```

minden swithen minden hálózat (vlan) kell, hogy át tudjon menni

ha a bpdu guard nem enged egy eszközt az egyik porton> int *port* > shutdown > no shutdown (kikapcs bekapcs)


SW1 (S1)
```
S1(config)#do show history

hostname S1

no ip domain-lookup

do terminal history size 250

line con 0

exec-timeout 0 0

logging synchronous

vlan 100

name Management

vlan 101

name Admin-LAN

vlan 102

name LAN-A

vlan 103

name LAN-B

vlan 999

name Native

vlan 1000

name Blackhole

exit

int range fa0/20-23

switchport mode access

switchport access vlan 101

switchport nonegotiate

spanning-tree portfast

spanning-tree bpduguard enable

exit

int vlan 100

description management interface

ip add 192.168.100.1 255.255.255.248

no shut

exit

ip default-gateway 192.168.100.6

do copy run start

int fa0/23

shutdown

no shut

do copy run start

show history

do show history

exit

int range fa0/24, gig0/2

switchport mode trunk

switchport nonegotiate

switchport trunk allowed vlan 100-103

switchport trunk native vlan 999

exit

do show vlan brief

int range fa0/1-19

switchport mode access

switchport nonegotiate

switchport access vlan 1000

shutdown

ecit

int gig0/1

switchport mode trunk

switchport nonegotiate

switchport trunk

switchport trunk allowed vlan 100-103

switchport trunk native vlan 999

exit

do copy run start

do show history
```


rendszerüzenetek letilása  (CDP: Cisco Discovery Protocol)
```
no cdp run
```


dhcp context: router kliens módba állítás nem a közvetlen első router ami osztja az IP címet
helperip
forrás 
forrás mac
ip cím (4 darab 255: limitált broadcast)

cisco 7.1.5 otthon

**kliens módba teszi a router**
```
int *interface*
ip address dhcp
no shut
```

slaac default default gateway:
fe80::1

AAA-ban a hitelesítés (authentication)
1.
```
line vty 0 04
password cisco login
```

2. ssh jelszó (ssh ver 2 vty 0 4, transport input ssh)


port security - sticky: elsőt megjegyzi, utána ennyi

cisco-nál a tdp-t kikapcsolni ha nem megbízható a hálózat


**Portbiztonság beállítása**
```
int range type *module/first-number* - *last-number*

int range fa0/8-24
shutdown
```


```
switchport port-security maximum *value*
```


nem használt portok lezárása

```
ip dhcp snooping
```



**Dollárjel fájlnév végén:** rejtett mappa



Packet tracer feladat működése

**research:**
- [ ] network address translation
- [ ] permit ip any any




```
BD1(config)#do show history

no ip domain-lookup

do terminal history size 250

line con 0

exec-timeout 0 0

logging synchronous

exir

ex

exit

enable secret Alfa1234@

ip domain-name szalezi.pt

crypto key gem rsa

crypto key gen rsa

hostname BD1

crypto key gen rsa

line vty 0 4

login local

transport input ssh

exit

int g0/0/0

does link to ISP

des link to ISP

ip add 203.0.113.6 255.255.255.240

no shut

exit

int g0/0/1

des link to szalezi LAN

ip add 172.20.10.1 255.255.255.240

ip add 172.20.10.1 255.255.255.2128

ip add 172.20.10.1 255.255.255.128

no shut

exit

do copy run start
```

**Alap ACL**
```
BD1(config)#ip access-list extended PAT_LIST

BD1(config-ext-nacl)#permit ip any any

BD1(config-ext-nacl)#exit
```

intranet server port: 

Can you co


putty jelszó: #Bb123456789@

linuxserverweb.xycompany.xy

Bok Péter Mikrotik setup:
network:
- bridged
- internal



W32tm /config /manualpeerlist:"0.hu.pool.ntp.org 1.hu.pool.ntp.org 2.hu.pool.ntp.org3.hu.pool.ntp.org" /syncfromflags:manual /reliable:yes /update


Install-ADDSFOREST -DomainName sulika.gg -DomainNetbiosName sulika -Force -DomainMode  7 -ForestMode 7 -InstallDns


windows server grafikusnál nem mindegy hogy domain name.el lépünk be vagy nem (távoli elérés)


Install-WindowsFeature DHCP -IncludeManagementTools


Add-DHCPServerV4Scope -name "scop1" -startrange 192.168.5.100 -endrange 192.168.5.121 -subnetmask 255.255.255.0

Set-DHCPServerV4OptionValue -dnsdomain sulika.gg -dnsserver 192.168.5.2 -router 192.168.5.1

Add-DHCPServerInDC -dnsname WADCORE1026GG.sulika.gg



Get-DnsServerResourceRecord -ZoneName "sulika.gg" -RRType "A"


Add-DnsServerResourceRecord -ZoneName "sulika.gg" -A -Name "www" -AllowUpdateAny -IPv4Address "192.168.5.3" -TimeToLive 01:00:00 -AgeRecord

Add-DnsServerResourceRecord -ZoneName "sulika.gg" -A -Name "ceg" -AllowUpdateAny -IPv4Address "192.168.5.3" -TimeToLive 01:00:00 -AgeRecord




**Windows file server setup**
graikuson jobb a megosztott mappa létrehozása mert az hozzá is adja

server manager >file storage>core server> shares> *jobb fent leyíló: task* new share> *E* meghajtón egy E:\diakozos directory (custom path) > permissions: customize > add> advanced> find now> vezetok>ok>full control bepipál>ok>share fül> kitöröl ami ott van> ugyanúgy vezetok hozzáadása > 8a 8b csoportokat csak olvasási joggal hozzáadás


tesztelése:
cmd \\gép




netsh interface ipv4 set address ethernet gateway=192.168.5.1





**Windows server core 2022 error 83 fix** 
```
Get-NetAdapter

Remove-NetIPAddress -InterfaceAlias Ethernet0 -confirm:$False

New-NetIPAddress -InterfaceAlias Ethernet0 -IPAddress 10.11.12.13 -PrefixLength 24 -DefaultGateway 10.11.12.1
```



kedd szerda 8 

PAT hoz kell egy ACL


SW1
```
SW1(config)#do show history
  login
  line vty 0 15
  password cisco2
  login
  exit
  service password-encryption
  banner motd "12J" Only!"
  copy run start
  exit
  do terminal history size 250
  no ip domain-lookup
  int range fa0/1 -2 
  switchport port-security
  switchport port-security maximum 1
  switchport port-security mac-address sitcky
  switchport port-security mac-address sticky
  switchport port-security violation restrict
  int range ffa0/3 - 24
  exit
  int range fa0/3 - 24
  int range fa0/3 - 24, gig0/1 - 2
  sh
  int range fa0/1 - 2
  no shut
  int vlan 1
  ip address 10.10.10.2 255.255.255.0
  no shut
  end
  do show history
SW1(config)#
```


SW2
```
SW1

no ip domain-lookup
do terminal history size 250
line con 0
exec-timeout 0 0
logging synchronous

int range gig0/1 - 2
switchport mode trunk
switchport nonegotiate 
vlan 100
name Native
interface range gig0/1 - 2
switchport trunk native vlan 100

interface range FastEthernet0/3-9, FastEthernet0/11-23
shutdown
exit

vlan 999
name Blackhole
exit

interface range FastEthernet0/3-9, FastEthernet0/11-23
switchport access vlan 999


interface range FastEthernet0/1, FastEthernet0/2, FastEthernet0/10,FastEthernet0/24
switchport mode access
switchport port-security


interface range FastEthernet0/1, FastEthernet0/2, FastEthernet0/10,FastEthernet0/24
switchport port-security maximum 4


interface FastEthernet0/1
switchport port-security mac-address 0010.11E8.3CBB


interface range FastEthernet0/1, FastEthernet0/2, FastEthernet0/10,FastEthernet0/24
switchport port-security mac-address sticky


switchport port-security mac-address 0010.11E8.3CBB
spanning-tree portfast
spanning-tree bpduguard enable

interface range FastEthernet0/2, FastEthernet0/10,FastEthernet0/24
ip dhcp snooping limit rate 5
switchport mode access
switchport port-security
switchport port-security maximum 4
switchport port-security mac-address sticky
switchport port-security violation restrict
spanning-tree portfast
spanning-tree bpduguard enable

interface range FastEthernet0/3-9, FastEthernet0/11-23
switchport access vlan 999
shutdown

interface range GigabitEthernet0/1-2
switchport trunk native vlan 100
ip dhcp snooping trust
switchport mode trunk
switchport nonegotiate
vlan 100
name Native
vlan 999
name BlackHole

interface range FastEthernet0/1, FastEthernet0/2, FastEthernet0/10,FastEthernet0/24
switchport port-security violation restrict



SW2

en
conf t
no ip domain-lookup
do terminal history size 250
line con 0
exec-timeout 0 0
logging synchronous

ip dhcp snooping
ip dhcp snooping vlan 10,20,99
spanning-tree portfast default
interface GigabitEthernet0/1
switchport trunk native vlan 100
switchport mode trunk
switchport nonegotiate

interface GigabitEthernet0/2
switchport trunk native vlan 100
switchport mode trunk
switchport nonegotiate

vlan 100
name Native
```

HF:




```
Install-ADDSFOREST -DomainName iskola.gg -DomainNetbiosName iskola -Force -DomainMode  7 -ForestMode 7 -InstallDns
```


```
Add-DHCPServerV4Scope -name "scop1" -startrange 192.168.7.100 -endrange 192.168.7.121 -subnetmask 255.255.255.0
```

```
Set-DHCPServerV4OptionValue -dnsdomain iskola.gg -dnsserver 192.168.7.2 -router 192.168.7.1
```

```
Add-DHCPServerInDC -dnsname WIN2022COREGG.iskola.gg
```

```
Add-DnsServerResourceRecord -ZoneName "iskola.gg" -A -Name "www" -AllowUpdateAny -IPv4Address "192.168.7.2" -TimeToLive 01:00:00 -AgeRecord
```

```
Get-DnsServerResourceRecord -ZoneName "iskola.gg" -RRType "A"
```

```
Remove-DnsServerResourceRecord -ZoneName "iskola.gg" -RRType "A" -Name "www"
```




Install-ADDSFOREST -DomainName sulika.gg -DomainNetbiosName sulika -Force -DomainMode  7 -ForestMode 7 -InstallDns


Add-DHCPServerV4Scope -name "scop1" -startrange 192.168.7.120 -endrange 192.168.7.139 -subnetmask 255.255.255.0


Set-DHCPServerV4OptionValue -dnsdomain sulika.gg -dnsserver 192.168.7.2 -router 192.168.7.1

Add-DHCPServerInDC -dnsname WIN2022COREGG.iskola.gg

vezető 4 ember
8 user összesen
csoportonlént 2-2 ebből 1-1 vezető

annyi mappa amennyi csoport
humán és szakma megosztása>figure out hozzáférés





dhcp scope

rsat utána tartomány


RSAT:
- active directory domain services
- DHCP server tools
- DNS server tools
- File Services tools
- group policy management tools
- server manager



show running-config interface gigabitEthernet0/1



```
interface range gigabitEthernet0/1-2
switchport trunk Native vlan 99
```


**alap vlan 1 tulajdonságai / vlan 1 properties**
- nem változhatható meg
- alpbeállításkent létrjön
- nem változhatható meg a neve
- 



AAAA:BBB:CCCC:2::0/64
192.168.3.0/24


network: 0.0.0.0 0.0.0.0 s0/0/0 nexthop vagy mindkettő

default ipv6 gateway
network ::/0s0/0/0




end
copy run start






Install-ADDSFOREST -DomainName iskola.gg -DomainNetbiosName iskola -Force -DomainMode  7 -ForestMode 7 -InstallDns

Add-DHCPServerV4Scope -name "scop1" -startrange 192.168.8.100 -endrange 192.168.8.121 -subnetmask 255.255.255.0

Set-DHCPServerV4OptionValue -dnsdomain iskola.gg -dnsserver 192.168.8.2 -router 192.168.8.1

Add-DHCPServerInDC -dnsname WADCORE1117GG.iskola.gg

set-DnsServerResourceRecord -ZoneName "iskola.gg" -A -Name "www" -AllowUpdateAny -IPv4Address "192.168.8.3" -TimeToLive 01:00:00 -AgeRecord


