# Lapres_Jarkom_A10_Modul5

Anggota :

Kana Rekha 05111840000001

Abdul Rozak Baharudin 05111840000148

# Soal A
* Membuat pembagian subnet seperti gambar berikut

![TOPO](https://user-images.githubusercontent.com/57948206/103259332-7f6d7280-49cb-11eb-9730-c66c711f9054.jpg)

* Menentukan jumlah alamat IP yang dibutuhkan oleh tiap subnet dan lakukan labelling netmask berdasarkan jumlah IP yang dibutuhkan

<img width="544" alt="TABEL IP" src="https://user-images.githubusercontent.com/57948206/103259330-7ed4dc00-49cb-11eb-98fb-abb64133577c.PNG">

* Menghitung pembagian IP berdasarkan NID dan netmask menggunakan pohon serta melakukan subnetting

![VLSM](https://user-images.githubusercontent.com/57948206/103259335-80060900-49cb-11eb-867b-2df6b27aeb87.jpg)

* IP SERVER
<img width="358" alt="IP SERVER" src="https://user-images.githubusercontent.com/57948206/103259328-7d0b1880-49cb-11eb-829e-ca28e0c3f017.PNG">

* Tabel Routing

<img width="519" alt="ROUTING" src="https://user-images.githubusercontent.com/57948206/103259329-7e3c4580-49cb-11eb-82e2-e989173b0e07.PNG">

# Soal B
* Membuat topologi.sh dan bye.sh

```
# Switch
uml_switch -unix switch0 > /dev/null < /dev/null &
uml_switch -unix switch1 > /dev/null < /dev/null &
uml_switch -unix switch2 > /dev/null < /dev/null &
uml_switch -unix switch3 > /dev/null < /dev/null &
uml_switch -unix switch4 > /dev/null < /dev/null &
uml_switch -unix switch5 > /dev/null < /dev/null &

# Router
xterm -T SURABAYA -e linux ubd0=SURABAYA,jarkom umid=SURABAYA eth0=tuntap,,,10.151.72.45 eth1=daemon,,,switch0 eth2=daemon,,,switch3 mem=96M &
xterm -T BATU -e linux ubd0=BATU,jarkom umid=BATU eth0=daemon,,,switch3 eth1=daemon,,,switch2 eth2=daemon,,,switch5 mem=96M &
xterm -T KEDIRI -e linux ubd0=KEDIRI,jarkom umid=KEDIRI eth0=daemon,,,switch0 eth1=daemon,,,switch1 eth2=daemon,,,switch4 mem=96M &

# Server
xterm -T PROBOLINGGO -e linux ubd0=PROBOLINGGO,jarkom umid=PROBOLINGGO eth0=daemon,,,switch1 mem=128M &
xterm -T MADIUN -e linux ubd0=MADIUN,jarkom umid=MADIUN eth0=daemon,,,switch1 mem=128M &
xterm -T MALANG -e linux ubd0=MALANG,jarkom umid=MALANG eth0=daemon,,,switch2 mem=128M &
xterm -T MOJOKERTO -e linux ubd0=MOJOKERTO,jarkom umid=MOJOKERTO eth0=daemon,,,switch2 mem=128M &

# Klien 1
xterm -T GRESIK -e linux ubd0=GRESIK,jarkom umid=GRESIK eth0=daemon,,,switch4 mem=96M &
xterm -T SIDOARJO -e linux ubd0=SIDOARJO,jarkom umid=SIDOARJO eth0=daemon,,,switch5 mem=96M &
```

```
uml_mconsole SURABAYA halt
uml_mconsole MALANG halt
uml_mconsole MOJOKERTO halt
uml_mconsole SIDOARJO halt
uml_mconsole GRESIK halt
uml_mconsole PROBOLINGGO halt
uml_mconsole KEDIRI halt
uml_mconsole BATU halt
uml_mconsole MADIUN halt
```

* Setting IP pada setiap UML dengan mengetikkan ``` nano /etc/network/interfaces ```
* interface pada UML SURABAYA
```
auto eth0
iface eth0 inet static
address 10.151.70.46
netmask 255.255.255.252
gateway 10.151.70.45
auto eth1
iface eth1 inet static
address 192.168.0.1
netmask 255.255.255.252
auto eth2
iface eth2 inet static
address 192.168.0.5
netmask 255.255.255.252
```
* interface pada UML BATU
```
auto eth0
iface eth0 inet static
address 192.168.0.6
netmask 255.255.255.252
gateway 192.168.0.5
auto eth1
iface eth1 inet static
address 10.151.71.89
netmask 255.255.255.248
auto eth2
iface eth2 inet static
address 192.168.2.1
netmask 255.255.255.0
```
* interface pada UML KEDIRI
```
auto eth0
iface eth0 inet static
address 192.168.0.2
netmask 255.255.255.252
gateway 192.168.0.1
auto eth1
iface eth1 inet static
address 192.168.0.9
netmask 255.255.255.248
auto eth2
iface eth2 inet static
address 192.168.1.1
netmask 255.255.255.0
```
* interface pada UML GRESIK
```
auto eth0
iface eth0 inet static
address 192.168.1.2
netmask 255.255.255.0
gateway 192.168.1.1
```
* interface pada UML MADIUN
```
auto eth0
iface eth0 inet static
address 192.168.0.10
netmask 255.255.255.248
gateway 192.168.0.9
```
* interface pada UML MALANG
```
auto eth0
iface eth0 inet static
address 10.151.71.90
netmask 255.255.255.248
gateway 10.151.71.89
```
* interface pada UML MOJOKERTO
```
auto eth0
iface eth0 inet static
address 10.151.71.91
netmask 255.255.255.248
gateway 10.151.71.89
```
* interface pada UML PROBOLINGGO
```
auto eth0
iface eth0 inet static
address 192.168.0.11
netmask 255.255.255.248
gateway 192.168.0.9
```
* interface pada UML SIDOARJO
```
auto eth0
iface eth0 inet static
address 192.168.2.2
netmask 255.255.255.0
gateway 192.168.2.1
```
# Soal C
* Melakukan routing agar setiap perangkat pada jaringan tersebut dapat terhubung dengan cara Membuat route.sh pada router SURABAYA
```
route add -net 192.168.1.0 netmask 255.255.255.0 gw 192.168.0.2
route add -net 192.168.2.0 netmask 255.255.255.0 gw 192.168.0.6
route add -net 192.168.0.8 netmask 255.255.255.248 gw 192.168.0.2
route add -net 10.151.71.88 netmask 255.255.255.248 gw 192.168.0.6
```
# Soal 1
Agar topologi yang kalian buat dapat mengakses keluar, kalian diminta untuk mengkonfigurasi SURABAYA menggunakan iptables, namun Bibah tidak ingin kalian menggunakan MASQUERADE.

**Penyelesaian**
* Pada UML SURABAYA memasukkan perintah sebagai berikut:
```
iptables -t nat -A POSTROUTING -s 192.168.0.0/22 -o eth0 -j SNAT --to-source 10.151.72.46
```
* Bila sudah, maka semua UML akan bisa ping ke its.ac.id

# Soal 2
Mendrop semua akses SSH dari luar Topologi (UML) Kalian pada server yang memiliki ip DMZ (DHCP dan DNS SERVER) pada SURABAYA demi menjaga keamanan.

**Penyelesaian**
* Pada UML SURABAYA memasukkan perintah sebagai berikut:
```
iptables -A FORWARD -d 10.151.73.88/29 -i eth0 -p tcp --dport 22 -j DROP
```
* Selanjutnya buka putty dan buat koneksi ssh ke uml MALANG dengan menuliskan berikut ```nc 10.151.73.90 22``` bila sudah terdrop maka pada putty tidak akan keluar seperti ini ```SSH-2.0-OpenSSH_6.0p1 Debian-4+deb7u4```
* Lalu pada MALANG ```nc -l -p 22``` untuk mengetes apakah dapat menerima packet yang datang
# Soal 3
Membatasi DHCP dan DNS server hanya boleh menerima maksimal 3 koneksi ICMP secara bersamaan yang berasal dari mana saja menggunakan iptables pada masing masing server, selebihnya akan di DROP.

**Penyelesaian**
* Pada UML MALANG & MOJOKERTO memasukkan perintah sebagai berikut:
```
iptables -A INPUT -p icmp -m connlimit --connlimit-above 3 --connlimit-mask 0 -j DROP
```
* Melakukan ping ke UML MALANG/MOJOKERTO ```ping 10.151.73.90``` dengan 4 UML yang berbeda, maka UML ke 4 tidak akan bisa melakukan ping ke MALANG
# Soal 4
Membatasi akses ke MALANG yang berasal dari SUBNET SIDOARJO dan SUBNET GRESIK dengan peraturan sebagai berikut:
* Akses dari subnet SIDOARJO hanya diperbolehkan pada pukul 07.00 - 17.00 pada hari Senin sampai Jumat .Selain itu paket akan di REJECT.

**Penyelesaian**
* Pada UML MALANG memasukkan perintah sebagai berikut:
```
iptables -A INPUT -s 192.168.2.0/24 -m time --timestart 07:00 --timestop 17:00 --weekdays Mon,Tue,Wed,Thu,Fri -j ACCEPT
```
```
iptables -A INPUT -s 192.168.2.0/24 -j REJECT
```
* untuk melakukan percobaan apakah bisa atau tidak, kita melakukan ```date``` lalu lihat apakah waktu di MALANG memenuhi syarat diakses oleh SIDOARJO
* untuk mencoba dengan waktu yang tidak bisa diakses, kita bisa melakukan ```date +%Y%m%d -s "20201229"``` dan ```date +%T -s "18:00:00"``` untuk mengganti waktu MALANG
# Soal 5
Membatasi akses ke MALANG yang berasal dari SUBNET SIDOARJO dan SUBNET GRESIK dengan peraturan sebagai berikut:
* Akses dari subnet GRESIK hanya diperbolehkan pada pukul 17.00 hingga pukul 07.00 setiap harinya.Selain itu paket akan di REJECT.

**Penyelesaian**
* Pada UML MALANG memasukkan perintah sebagai berikut:
```
iptables -A INPUT -s 192.168.1.0/24 -m time --timestart 07:00 --timestop 17:00 -j REJECT
```
* untuk melakukan percobaan apakah bisa atau tidak, kita melakukan ```date``` lalu lihat apakah waktu di MALANG memenuhi syarat diakses oleh GRESIK
* untuk mencoba dengan waktu yang bisa diakses, kita bisa melakukan ```date +%Y%m%d -s "20201229"``` dan ```date +%T -s "18:00:00"``` untuk mengganti waktu MALANG
# Soal 7
Semua paket didrop oleh firewall (dalam topologi) tercatat dalam log pada setiap UML yang memiliki aturan drop.

**Penyelesaian**
* Pada UML MALANG, MOJOKERTO, dan SURABAYA membuat file no7.sh lalu memasukkan perintah seperti gambar dibawah ini .
```
iptables -N LOGGING
iptables -A INPUT -j LOGGING
iptables -A OUTPUT -j LOGGING
iptables -A LOGGING -j LOG --log-prefix "IPTables-Dropped: " --log-level 4
iptables -A LOGGING -j DROP
```
* Lalu ping salah satu IP MALANG, MOJOKERTO, atau SURABAYA di UML lain .
* Pada contoh dibawah ini testing IP SURABAYA di UML SIDOARJO . Hasilnya akan seperti gambar berikut ini :
<img width="367" alt="7" src="https://user-images.githubusercontent.com/57948206/103260555-a8dccd00-49d0-11eb-9d7a-d43ed0c1516c.PNG">

