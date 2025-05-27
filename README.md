DEBIAN AWS
1.	Szerver létrehozása az AWS felületén:
a.	Hozzon létre egy Debian alapú virtuális szervert és indítsa el.
b.	A gép neve: Debian-AWS legyen.
EC2 → Launch instance → név, Debian, t2.micro, HTTP+HTTPS enable
Create new key pair → név + rsa + .ppk → Launch instance











2.	Rendeljen hozzá egy publikus statikus IP címet a szerverhez
a.	Az AWS megfelelő felületén rendeljen hozzá egy statikus IP címet a Debian szerverhez.
b.	Készítsen képernyőmentést a beállításokról!
Elastic IPs → bepipál → Allocate IP address → tag nevet megad → Allocate 

3.	Engedélyezze az AWS-ben a biztonsági beállításokban, hogy a gép bármely külső címről és bármely porton keresztül elérhető legyen.
a.	Készítsen képernyőmentést a beállításokról!
Security Groups → launch-wizard-1 bepipál → inbound rules → edit → add rule → 
All traffic + Anywhere IPv4




Public IPv4-et kimásol → Putty cím bemásol → SSH → Auth → Credentials →
Private key file-t feltölt
Login as: admin
sudo -s
*mindent letölteni*
4.	Webszerver telepítése, konfigurálása:
a.	Telepítsen egy Apache webszervert és konfigurálja be.
b.	Az alapértelmezett oldal helyett készítsen egy új oldalt, amely valamilyen színes hátteren egy linket tartalmaz a www.zipernowsky.hu oldalra, illetve a saját nevét, a Debian szót és a maidátumot. 
c.	Készítsen a beállításokról képernyőmentést, lehetőleg a gazdagép böngészőjéből!
/var/www/html/index.html-t átírni vagy törölni és újraírni

5.	A DHCP kiszolgáló telepítése:
a.	A tartományban 40 számítógép van, ezért egy 64-es tartományt (Range) állítson be. Használja azt a belső IP tartományt, amelyet az AWS-től kapott a számítógép.
b.	Állítsa be az átjárót a tartomány első IP címére.
c.	DNS szerverek IP címe a 8.8.8.8 és 8.8.4.4 legyen
d.	A tartomány aws01.local legyen
e.	A bérleti idő 1111 mp, a maximális bérleti idő 2222 mp legyen
f.	A szerver legyen authoritative módban.
g.	Készítsen a beállításokról képernyőmentést!
/etc/dhcp/dhcpd.conf ↓




6.	Tűzfal beállítása:
a.	Telepítse fel az iptables-t.
b.	Dobja el a localhost címre érkező ping (ICMP) csomagokat a tűzfal segítségével!
c.	Engedélyezze az FTP kapcsolatot.
d.	Engedélyezze a HTTP kapcsolatot.
e.	Engedélyezze a DNS szervert.
f.	Készítsen a beállításokról képernyőmentést!
iptables -A INPUT -d 127.0.0.1 -p icmp --icmp-type echo-request -j DROP
sudo iptables -A INPUT -p tcp --dport 21 -j ACCEPT
sudo iptables -A INPUT -p tcp --dport 20 -j ACCEPT
sudo iptables -A INPUT -p tcp --dport 80 -j ACCEPT
sudo iptables -A INPUT -p udp --dport 53 -j ACCEPT
sudo iptables -A INPUT -p tcp --dport 53 -j ACCEPT
7.	Konfigurálja be a Debian szervert, hogy az az alábbi névszervereket használja:
a.	8.8.8.8
b.	8.8.4.4
c.	Készítsen a beállításokról képernyőmentést!
d.	
8.	etc/dhcp/dhclient.conf ↓
a.	/etc/resolv.conf ↓
9.	Samba megosztás készítése
a.	Telepítse fel a Samba szervert.
b.	Készítsen egy tetszőleges megosztást Samba segítségével.
c.	Készítsen képernyőmentést a beállításokról!

etc/samba/smb.conf ↓


