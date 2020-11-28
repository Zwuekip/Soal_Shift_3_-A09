# Soal_Shift_3_A09

### Kelompok A09:
- Iman Afandy (05111740000129)
- Nodas Uziel Putra Serpara (5111840007007)

## DHCP
##  Nomor 1
<p>Yaitu untuk membuat topologi jaringan demi kelancaran TA-nya dengan kriteria sebagai berikut:</p> 
<br>
<img src="Gambar/18.png" width="600">
<br>
<p>  Anri sudah pernah mempelajari teknik Jaringan Komputer sehingga Anri dapat membuat topologi tersebut dengan mudah. Bu Meguri memerintahkan Anri untuk menjadikan SURABAYA sebagai router, MALANG sebagai DNS Server, TUBAN sebagai DHCP server, serta MOJOKERTO sebagai Proxy server, dan UML lainnya sebagai client. Bu Meguri berpesan pada Anri untuk menyusun topologi secara hati-hati dan memperhatikan gambar topologi yang diberikan Bu Meguri. Karena TUBAN jauh dari client, maka perlu adanya perantara agar bisa saling terhubung. </p>

#### Jawab 
<p>1. Mengedit Topologi menjadi :</p> 

```
# Switch
uml_switch -unix switch1 > /dev/null < /dev/null &
uml_switch -unix switch2 > /dev/null < /dev/null &
uml_switch -unix switch3 > /dev/null < /dev/null &

# Router
xterm -T SURABAYA -e linux ubd0=SURABAYA,jarkom umid=SURABAYA eth0=tuntap,,,10.151.72.41 eth1=daemon,,,switch1 eth2=daemon,,,switch3 eth3=daemon,,,switch2 mem=256M &

# Server
xterm -T MALANG -e linux ubd0=MALANG,jarkom umid=MALANG eth0=daemon,,,switch2 mem=160M &
xterm -T MOJOKERTO -e linux ubd0=MOJOKERTO,jarkom umid=MOJOKERTO eth0=daemon,,,switch2 mem=128M &
xterm -T TUBAN -e linux ubd0=TUBAN,jarkom umid=TUBAN eth0=daemon,,,switch2 mem=128M &

# Klien
xterm -T BANYUWANGI -e linux ubd0=BANYUWANGI,jarkom umid=BANYUWANGI eth0=daemon,,,switch3 mem=64M &
xterm -T SIDOARJO -e linux ubd0=SIDOARJO,jarkom umid=SIDOARJO eth0=daemon,,,switch1 mem=64M &
xterm -T GRESIK -e linux ubd0=GRESIK,jarkom umid=GRESIK eth0=daemon,,,switch1 mem=64M &
xterm -T MADIUN -e linux ubd0=MADIUN,jarkom umid=MADIUN eth0=daemon,,,switch3 mem=64M &
```
<p>2. Menghapus # pada IP Forward di sysctl.conf (SURABAYA)</p> 

```
nano /etc/sysctl.conf (surabaya)
uncomment net.ipv4.ip_forward=1
sysctl -p
```
<br>
<img src="Gambar/16.png" width="600">
<br>
<p>3. Membuat Interface </p> 

<p>4. Melakukan Iptable di Surabaya </p> 

```
iptables -t nat -A POSTROUTING -o eth0 -j MASQUERADE -s 192.168.0.0/16
```

## Nomor 2 


## Nomor 3 
## Nomor 4 
## Nomor 5 
## Nomor 6 
## Nomor 7 
