[![Review Assignment Due Date](https://classroom.github.com/assets/deadline-readme-button-22041afd0340ce965d47ae6ef1cefeee28c7c493a6346c4f15d667ab976d596c.svg)](https://classroom.github.com/a/B4ZON9Qp)


| Name           | NRP        | Kelas     |
| --- | --- | --- |
| Maleka Ghaniya | 5025241189 | JARKOM A  |




## Put your topology config image here!

![alt](https://github.com/Maleka0809/FP_JARKOM/blob/9a95cc8f667094291b23a5ca70eb13133a1c7b44/Screenshot%202025-12-07%20113007.png)

## Put your GNS3 Project file here!
[link](https://github.com/Maleka0809/jarkom_praktikum_4/blob/23e60b90e1be8f5b7e0b7124f7846d2fa75a4f77/final_praktikum_Maleka.gns3project)


## Soal 1

> Menggunakan metode VLSM, buatlah pembagian subnet untuk masing-masing gedung dengan cara yang seefisien mungkin!

> _Using the VLSM method, create subnets for each building as efficiently as possible!_

**Answer:**

- Screenshot


  ![alt](https://github.com/Maleka0809/FP_JARKOM/blob/92ef9f90a63fe95c3a9b0aa29b1ac0196d3ed0dd/vlsm2.jpg)
  ![alt](https://github.com/Maleka0809/FP_JARKOM/blob/36591690218348264718a11e9f470c4ee0e4f293/vlsm3.jpg)

- Explanation


| Nama Subnet | CIDR | Netmask | Network ID | IP Gateway (Router) | Range IP Usable | Broadcast IP |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| **Client-Group-3** | `/19` | 255.255.224.0 | `10.58.0.0` | 10.58.0.1 | 10.58.0.2 - 10.58.31.254 | 10.58.31.255 |
| **Client-Group-2** | `/21` | 255.255.248.0 | `10.58.32.0` | 10.58.32.1 | 10.58.32.2 - 10.58.39.254 | 10.58.39.255 |
| **Client-Group-1** | `/24` | 255.255.255.0 | `10.58.40.0` | 10.58.40.1 | 10.58.40.2 - 10.58.40.254 | 10.58.40.255 |
| **Webserver-Group-2** | `/24` | 255.255.255.0 | `10.58.41.0` | 10.58.41.1 | 10.58.41.2 - 10.58.41.254 | 10.58.41.255 |
| **Webserver-Group-1** | `/25` | 255.255.255.128 | `10.58.42.0` | 10.58.42.1 | 10.58.42.2 - 10.58.42.126 | 10.58.42.127 |
| **DHCP-Group-1** | `/26` | 255.255.255.192 | `10.58.42.128` | 10.58.42.129 | 10.58.42.130 - 10.58.42.190 | 10.58.42.191 |
| **DNS-Group-1** | `/28` | 255.255.255.240 | `10.58.42.192` | 10.58.42.193 | 10.58.42.194 - 10.58.42.206 | 10.58.42.207 |
| **Backbone (Pusat)** | `/29` | 255.255.255.248 | `10.58.42.208` | *Multi-Router* | 10.58.42.209 - 10.58.42.214 | 10.58.42.215 |
| **DMZ (Petrov)** | `/29` | 255.255.255.248 | `10.58.42.216` | 10.58.42.217 | 10.58.42.218 - 10.58.42.222 | 10.58.42.223 |
| **P2P (Fianchetto)** | `/30` | 255.255.255.252 | `10.58.42.224` | *P2P* | 10.58.42.225 - 10.58.42.226 | 10.58.42.227 |
| **P2P (Zwischen)** | `/30` | 255.255.255.252 | `10.58.42.228` | *P2P* | 10.58.42.229 - 10.58.42.230 | 10.58.42.231 |


  Metode VLSM (Variable Length Subnet Masking) digunakan untuk menghemat alamat IP dengan menyesuaikan ukuran subnet berdasarkan kebutuhan host yang sebenarnya, dimulai dari subnet yang membutuhkan host terbanyak. Ini mencegah pemborosan IP yang besar dibandingkan metode FLSM.

<br>

## Soal 2

> Konfigurasi semua router agar bisa terhubung ke semua jaringan. Gunakan static routing dan uji dengan melakukan ping dari **Budapest** ke **Alekhine** dan dari **Ponziani** ke **Sicilian**!

> _Configure all routers to connect to all networks. Use static routing and perform testing by pinging from **Budapest** to **Alekhine** and from **Ponziani** to **Sicilian**!_

**Answer:**

- Screenshot

 ![alt](https://github.com/Maleka0809/FP_JARKOM/blob/9a95cc8f667094291b23a5ca70eb13133a1c7b44/Screenshot%202025-12-07%20114136.png)
 ![alt](https://github.com/Maleka0809/FP_JARKOM/blob/9a95cc8f667094291b23a5ca70eb13133a1c7b44/Screenshot%202025-12-07%20114028.png)

- Explanation
  Static Routing digunakan untuk membangun konektivitas end-to-end antar subnet. Setiap router diatur untuk mengetahui jalur menuju subnet yang tidak terhubung langsung, dengan menentukan IP next-hop (alamat router tetangga) yang spesifik.

 ###### Budapest
```
auto eth0
iface eth0 inet static
    address 10.58.40.2
    netmask 255.255.255.0
    gateway 10.58.40.1
```
###### Ponziani
```
auto eth0
iface eth0 inet static
	address 10.58.42.130
	netmask 255.255.255.192
	gateway 10.58.42.129
```
###### Sicilian
```
auto eth0
iface eth0 inet static
	address 10.58.42.2
	netmask 255.255.255.128
	gateway 10.58.42.1
```
###### Alekhine
```
auto eth0
iface eth0 inet static
	address 10.58.42.194
	netmask 255.255.255.240
	gateway 10.58.42.193
```
###### Slav
```
auto eth0
iface eth0 inet static
	address 10.58.41.2
	netmask 255.255.255.0
	gateway 10.58.41.1
```

###### Smith Morra
```
auto lo
iface lo inet loopback
    up sysctl -w net.ipv4.ip_forward=1

# eth0: KE INTERNET (NAT) - Sesuai gambar
auto eth0
iface eth0 inet dhcp

# eth1: KE FIANCHETTO (Uplink)
auto eth1
iface eth1 inet static
    address 10.58.42.226
    netmask 255.255.255.252
    # Default Route (Semua paket lempar ke atas)
    up ip route add 0.0.0.0/0 via 10.58.42.225

# eth2: KE SWITCH-G-1 (Arah Budapest)
# Pastikan kabel dari Switch-G-1 nyolok ke eth2
auto eth2
iface eth2 inet static
    address 10.58.40.1
    netmask 255.255.255.0

# eth3: KE SWITCH-G-2 (Arah Client Group 2 & 3)
auto eth3
iface eth3 inet static
    address 10.58.0.1
    netmask 255.255.224.0


```
###### Fianchetto
```
auto lo
iface lo inet loopback
    up sysctl -w net.ipv4.ip_forward=1

# eth0: KE BACKBONE
auto eth0
iface eth0 inet static
    address 10.58.42.210
    netmask 255.255.255.248
    up ip route add 10.58.42.128/26 via 10.58.42.209
    
    # Rute ke Gedung D (Web1, Web2, DNS, DMZ)
    up ip route add 10.58.41.0/24 via 10.58.42.211
    up ip route add 10.58.42.0/25 via 10.58.42.211
    up ip route add 10.58.42.192/28 via 10.58.42.211
    up ip route add 10.58.42.216/29 via 10.58.42.211
    # HAPUS RUTE .228/30 KARENA TIDAK DIPAKAI LAGI

# eth1: KE SMITH-MORRA
auto eth1
iface eth1 inet static
    address 10.58.42.225
    netmask 255.255.255.252
    up ip route add 10.58.0.0/19 via 10.58.42.226
    up ip route add 10.58.32.0/21 via 10.58.42.226
    up ip route add 10.58.40.0/24 via 10.58.42.226
```
###### Lucena
```
auto lo
iface lo inet loopback
    up sysctl -w net.ipv4.ip_forward=1

# eth0: KE SWITCH-O (Gedung O / Ponziani)
# Sesuai gambar: Kabel ke kiri adalah eth0
auto eth0
iface eth0 inet static
    address 10.58.42.129
    netmask 255.255.255.192

# eth1: KE BACKBONE (Switch-Pusat)
# Sesuai gambar: Kabel ke kanan adalah eth1
auto eth1
iface eth1 inet static
    address 10.58.42.209
    netmask 255.255.255.248
    
    # RUTE KE GEDUNG G (Lewat Fianchetto .210)
    up ip route add 10.58.0.0/18 via 10.58.42.210

    # RUTE KE GEDUNG D (Lewat Zwischenzug .211)
    up ip route add 10.58.41.0/24 via 10.58.42.211
    up ip route add 10.58.42.0/25 via 10.58.42.211
    up ip route add 10.58.42.192/28 via 10.58.42.211
    up ip route add 10.58.42.216/29 via 10.58.42.211
```
###### Zwischenzug
```
auto lo
iface lo inet loopback
    up sysctl -w net.ipv4.ip_forward=1

# eth0: KE BACKBONE (Switch-Pusat)
auto eth0
iface eth0 inet static
    address 10.58.42.211
    netmask 255.255.255.248
    
    # Rute Balik ke Gedung O & G
    up ip route add 10.58.42.128/26 via 10.58.42.209
    up ip route add 10.58.0.0/18 via 10.58.42.210

# eth1: KE SWITCH-D (Jalur ke Petrov & Zugzwang)
auto eth1
iface eth1 inet static
    address 10.58.42.218
    netmask 255.255.255.248
    
    # RUTE KE BAWAH (ZUGZWANG .220)
    # Karena Sicilian, Slav, Alekhine ada di bawah Zugzwang, kita oper ke dia.
    up ip route add 10.58.41.0/24 via 10.58.42.220
    up ip route add 10.58.42.0/25 via 10.58.42.220
    up ip route add 10.58.42.192/28 via 10.58.42.220
```
###### Zugzwang
```
auto lo
iface lo inet loopback
    up sysctl -w net.ipv4.ip_forward=1

# eth0: KE SWITCH-D (Uplink ke Zwischenzug)
auto eth0
iface eth0 inet static
    address 10.58.42.220
    netmask 255.255.255.248
    gateway 10.58.42.218

# eth1: KE SICILIAN (Webserver 1) - KOREKSI KAMU
auto eth1
iface eth1 inet static
    address 10.58.42.1
    netmask 255.255.255.128

# eth2: KE ALEKHINE (DNS) - KOREKSI KAMU
auto eth2
iface eth2 inet static
    address 10.58.42.193
    netmask 255.255.255.240

# eth3: KE SLAV (Webserver 2) - KOREKSI KAMU
auto eth3
iface eth3 inet static
    address 10.58.41.1
    netmask 255.255.255.0

```

<br>

## Soal 3

> Berikan seluruh client (**Blackmar-Diemer, Budapest,** dan **Stafford**) IP secara dinamis dari DHCP. Range IP dibebaskan, namun tunjukkan bahwa mereka mendapatkan IP secara dinamis!

> _Assign all clients (**Blackmar-Diemer, Budapest,** and **Stafford**) dynamic IP addresses via DHCP. You may use any IP range you would like, but prove that they receive IP addresses dynamically!_

**Answer:**

- Screenshot

 ![alt](https://github.com/Maleka0809/FP_JARKOM/blob/43d13f58ee4cb32259c9d3b9f6a7438f9cd4281a/Screenshot%202025-12-07%20152135.png)
![alt](https://github.com/Maleka0809/FP_JARKOM/blob/43d13f58ee4cb32259c9d3b9f6a7438f9cd4281a/Screenshot%202025-12-07%20152223.png)
![alt](https://github.com/Maleka0809/FP_JARKOM/blob/43d13f58ee4cb32259c9d3b9f6a7438f9cd4281a/Screenshot%202025-12-07%20152229.png)
- Explanation
  DHCP dinamis diimplementasikan dengan mengkonfigurasi Ponziani sebagai DHCP Server dan Smith-Morra sebagai DHCP Relay . DHCP Relay diperlukan agar permintaan DHCPDISCOVER dari klien dapat melewati router dan mencapai server di subnet yang berbeda.
  
###### Ponziani
```
auto eth0
iface eth0 inet static
    address 10.58.42.130
    netmask 255.255.255.192
    gateway 10.58.42.129
    up echo nameserver 8.8.8.8 > /etc/resolv.conf

    # 1. AUTO INSTALL (Silent Mode)
    post-up apt-get update -qq || true
    post-up DEBIAN_FRONTEND=noninteractive apt-get install isc-dhcp-server -y -qq || true

    # 2. AUTO CONFIG: Tentukan Interface
    post-up echo 'INTERFACESv4="eth0"' > /etc/default/isc-dhcp-server

    # 3. AUTO CONFIG: Inject Aturan Subnet ke dhcpd.conf
    # (Kita pakai 'echo' beruntun biar aman)
    post-up echo 'default-lease-time 600;' > /etc/dhcp/dhcpd.conf
    post-up echo 'max-lease-time 7200;' >> /etc/dhcp/dhcpd.conf
    post-up echo 'option domain-name-servers 10.58.42.194, 10.58.42.195;' >> /etc/dhcp/dhcpd.conf
    
    # Subnet Lokal Ponziani (Wajib)
    post-up echo 'subnet 10.58.42.128 netmask 255.255.255.192 {}' >> /etc/dhcp/dhcpd.conf
    
    # Subnet Client Group 1 (Budapest)
    post-up echo 'subnet 10.58.40.0 netmask 255.255.255.0 {' >> /etc/dhcp/dhcpd.conf
    post-up echo '  range 10.58.40.10 10.58.40.100;' >> /etc/dhcp/dhcpd.conf
    post-up echo '  option routers 10.58.40.1;' >> /etc/dhcp/dhcpd.conf
    post-up echo '}' >> /etc/dhcp/dhcpd.conf

    # Subnet Client Group 2 & 3 (Blackmar)
    post-up echo 'subnet 10.58.0.0 netmask 255.255.224.0 {' >> /etc/dhcp/dhcpd.conf
    post-up echo '  range 10.58.0.10 10.58.0.100;' >> /etc/dhcp/dhcpd.conf
    post-up echo '  option routers 10.58.0.1;' >> /etc/dhcp/dhcpd.conf
    post-up echo '}' >> /etc/dhcp/dhcpd.conf

    # 4. RESTART SERVICE
    post-up sleep 5 && service isc-dhcp-server restart
```
###### Smith Morra
```
auto lo
iface lo inet loopback
    # Aktifkan IP Forwarding
    up echo 1 > /proc/sys/net/ipv4/ip_forward

# --- INTERNET & INSTALLER (eth0) ---
# Di sini kita lakukan semua installasi karena ini sumber internet
auto eth0
iface eth0 inet dhcp
    # DNS Google biar apt jalan
    up echo nameserver 8.8.8.8 > /etc/resolv.conf
    
    # 1. Update & Install (Pakai mode silent/noninteractive biar gak macet)
    post-up apt-get update -qq || true
    post-up DEBIAN_FRONTEND=noninteractive apt-get install iptables isc-dhcp-relay -y -qq || true
    
    # 2. Aktifkan NAT (Masquerade) - AGAR INTERNET JALAN
    post-up iptables -t nat -A POSTROUTING -o eth0 -j MASQUERADE
    
    # 3. Konfigurasi DHCP RELAY (Inject IP Server PONZIANI Kamu)
    # Server: 10.58.42.130 (Ponziani)
    # Interfaces: eth1 (uplink), eth2 (client1), eth3 (client2&3)
    post-up echo 'SERVERS="10.58.42.130"' > /etc/default/isc-dhcp-relay
    post-up echo 'INTERFACES="eth1 eth2 eth3"' >> /etc/default/isc-dhcp-relay
    post-up echo 'OPTIONS=""' >> /etc/default/isc-dhcp-relay

# --- KONFIGURASI ROUTING & CLIENT ---

# eth1: UPLINK KE FIANCHETTO
auto eth1
iface eth1 inet static
    address 10.58.42.226
    netmask 255.255.255.252
    
    # Routing ke Gedung O & D (Lewat Fianchetto)
    # Kita pakai rangkuman (Summary) biar script gak kepanjangan
    up ip route add 10.58.42.128/26 via 10.58.42.225 || true
    up ip route add 10.58.42.0/23 via 10.58.42.225 || true

# eth2: CLIENT GROUP 1
auto eth2
iface eth2 inet static
    address 10.58.40.1
    netmask 255.255.255.0

# eth3: CLIENT GROUP 2 & 3
# Kita restart service di interface terakhir biar aman
auto eth3
iface eth3 inet static
    address 10.58.0.1
    netmask 255.255.224.0
    
    # Restart Relay setelah semua interface UP
    post-up sleep 10 && service isc-dhcp-relay restart
```

<br>

## Soal 4

> Berikan web server **Slav** dan **Sicilian** IP address yang tetap/fixed dari DHCP. 

> _Assign **Slav** and **Sicilian** web servers fixed IP addresses via DHCP._

**Answer:**

- Screenshot

  ![alt](https://github.com/Maleka0809/FP_JARKOM/blob/1a0d5fc04b77045306bcc324283cb28c5e9a3299/Screenshot%202025-12-07%20233744.png)
  ![alt](https://github.com/Maleka0809/FP_JARKOM/blob/1a0d5fc04b77045306bcc324283cb28c5e9a3299/Screenshot%202025-12-07%20233842.png)

- Explanation

  IP Fixed dicapai melalui DHCP Reservasi pada server Ponziani. DHCP Server mengikat MAC Address unik perangkat ke alamat IP tertentu, memastikan perangkat tersebut selalu menerima IP yang sama.

```
  // Reservasi untuk Sicilian (10.58.42.2)
post-up echo 'host Sicilian {' >> /etc/dhcp/dhcpd.conf
post-up echo '    hardware ethernet 02:42:f0:ce:bf:00;' >> /etc/dhcp/dhcpd.conf
post-up echo '    fixed-address 10.58.42.2;' >> /etc/dhcp/dhcpd.conf
post-up echo '}' >> /etc/dhcp/dhcpd.conf

// Reservasi untuk Slav (10.58.41.2)
post-up echo 'host Slav {' >> /etc/dhcp/dhcpd.conf
post-up echo '    hardware ethernet 02:42:f4:e5:89:00;' >> /etc/dhcp/dhcpd.conf
post-up echo '    fixed-address 10.58.41.2;' >> /etc/dhcp/dhcpd.conf
post-up echo '}' >> /etc/dhcp/dhcpd.conf
  
```

<br>

## Soal 5

> Buatlah konfigurasi untuk domain:  
**parkov.com** → IP Node **Slav**  
**paskarov.com** → IP Node **Sicilian** 
Pada **DNS Master Caro-Kann.** Tambahkan juga subdomain www untuk kedua domain tersebut.

> _Configure the domains:  
**parkov.com** → **Slav** Node IP  
**paskarov.com** → **Sicilian** Node IP  
On the **Caro-Kann DNS Master,** then add the www subdomain for both domains._

**Answer:**

- Screenshot

  ![alt](https://github.com/Maleka0809/FP_JARKOM/blob/a033de3268fb70ac29e833ca0402ed4502cd50e6/Screenshot%202025-12-07%20235337.png)

- Explanation

Caro-Kann dikonfigurasi sebagai DNS Master. A Record (A) memetakan domain ke IP, sementara Canonical Name (CNAME) digunakan untuk membuat alias (www) yang menunjuk ke nama domain utama.

###### Caro-Kann 
```
paskarov     IN    A    10.58.42.2      ; IP Sicilian
www          IN    CNAME paskarov.com.

parkov       IN    A    10.58.41.2      ; IP Slav
www          IN    CNAME parkov.com.
```

<br>

## Soal 6

> Konfigurasikan juga **Alekhine** sebagai **DNS Slave** yang bekerja untuk membantu **Caro-Kann.** Lakukan pengujian dengan **mematikan Caro-Kann** lalu coba ping ke domain dan subdomain tersebut (pilih salah satu saja).

> _Configure **Alekhine** as a **DNS Slave** to assist **Caro-Kann**. Perform testing by **disabling Caro-Kann** and then pinging the domain and subdomain (choose only one)._

**Answer:**

- Screenshot

![alt](https://github.com/Maleka0809/FP_JARKOM/blob/7e6767bafc2685cd5da77f481bb11bac39ebe397/Screenshot%202025-12-07%20235456.png)

- Explanation
  Alekhine dikonfigurasi sebagai DNS Slave (type slave) untuk memberikan redundansi. Saat Caro-Kann (Master) dimatikan, Alekhine tetap dapat melayani permintaan resolusi domain menggunakan data zona yang telah disalin (Zone Transfer).
  ##### Alekahine
```
zone "parkov.com" {
    type slave;
    // File ini adalah hasil salinan zona
    file "/var/lib/bind/parkov.com.db";
    // Menunjuk IP Caro-Kann (Master) sebagai sumber
    masters { 10.58.42.195; }; 
};
```

<br>

## Soal 7

> Konfigurasikan **Sicilian** agar berfungsi sebagai **web server nginx** yang akan menyajikan [halaman berikut](https://drive.google.com/file/d/1eX0ZjRKprx8T34XFAssrpc7ZE1j6Jv0j/view). Konfigurasikan juga agar **Sicilian** bisa menyimpan custom access log ke file **/tmp/access.log** dan error log ke file **/tmp/error.log.**

> _Configure **Sicilian** to function as an **nginx web server**that will serve [this page](https://drive.google.com/file/d/1eX0ZjRKprx8T34XFAssrpc7ZE1j6Jv0j/view). Also, configure **Sicilian** to save custom access logs to **/tmp/access.log** and error logs to **/tmp/error.log.**_

**Answer:**

- Screenshot

  ![alt](https://github.com/Maleka0809/FP_JARKOM/blob/a9f095a49c34f0f374abb366a09bfa6b0a18f950/Screenshot%202025-12-09%20130042.png)

- Explanation

  Sicilian menjalankan Nginx dan melayani domain di port 80 standar. Logging diatur ke path kustom (/myscripts/tmp/) untuk tujuan Soal 8.
```
  server {
    listen 80;
    server_name paskarov.com;

    // SOAL 7: Penentuan path log custom
    access_log /myscripts/tmp/access.log jarkom_format;
    error_log /myscripts/tmp/error.log;

    root /myscripts/myweb/sicilian; 
    index sicilian.html;
}
```

<br>

## Soal 8

> Buatlah custom access log ke file **/tmp/access.log.** Untuk keperluan logging, gunakan format log seperti di bawah:
> - Tanggal dan waktu akses dalam format standar log.
> - Nama node yang sedang diakses.
> - Alamat IP klien yang mengakses website.
> - Metode HTTP dan URI yang diakses oleh klien.
> - Status respons HTTP yang diberikan oleh server.
> - Jumlah byte yang dikirimkan dalam respons.
> - Waktu yang dihabiskan oleh server untuk menangani permintaan.> 
> - Contoh format log yang sesuai:  
[01/Oct/2024:11:30:45 +0000] Jarkom Node Sicilian Access from 192.168.1.15 using method "GET /resep/bayam HTTP/1.1" returned status 200 with 2567 bytes sent in 0.038 seconds

> _Webserver: Create a custom access log to the file **/tmp/access.log.** For logging purposes, use the log format shown below:_
> - _The date and time of access in standard log format._
> - _The name of the node being accessed._
> - _The IP address of the client accessing the website._
> - _The HTTP method and URI accessed by the client._
> - _The HTTP response status returned by the server._
> - _The number of bytes sent in the response._
> - _The time spent by the server processing the request._
> - _Example of appropriate log format:  
[01/Oct/2024:11:30:45 +0000] Jarkom Node Sicilian Access from 192.168.1.15 using method "GET /resep/bayam HTTP/1.1" returned status 200 with 2567 bytes sent in 0.038 seconds_

**Answer:**

- Screenshot

  ![alt](https://github.com/Maleka0809/FP_JARKOM/blob/dc1557d2bad46a2ac6f0d2e51ce510569a802459/Screenshot%202025-12-09%20131040.png)

- Explanation

  Custom Logging dibuat menggunakan direktif log_format di Nginx (Sicilian). Format ini menggunakan variabel internal Nginx seperti $remote_addr (IP Klien), $request (Metode dan URI), dan $request_time (Waktu pemrosesan) untuk mencatat detail yang diminta.

```
http {
    // SOAL 8: Definisi format log kustom dengan variabel Nginx
    log_format jarkom_format '$time_local Jarkom Node Sicilian Access from $remote_addr using method "$request" returned status $status with $body_bytes_sent bytes sent in $request_time seconds';
    
    // ...
}
``` 

<br>

## Soal 9

> Konfigurasikan juga **Slav** agar berfungsi sebagai **web server nginx** yang menyajikan [halaman berikut](https://drive.google.com/file/d/1h8ik1Zcubntp0dvHt9NHYqSZLSTG6FuZ/view) dan **hanya** bisa diakses melalui port **8000** dan **8888.**

> _Configure **Slav** to function as an **nginx web server** that serves [this page](https://drive.google.com/file/d/1h8ik1Zcubntp0dvHt9NHYqSZLSTG6FuZ/view?usp=drive_link) and is **only** accessible via ports **8000** and **8888.**_

**Answer:**

- Screenshot
##### Port 8000
  ![alt](https://github.com/Maleka0809/FP_JARKOM/blob/56864f5beee072ae8d0ae91c69e6727455e89552/Screenshot%202025-12-09%20131308.png)
##### Port 8888
  ![alt](https://github.com/Maleka0809/FP_JARKOM/blob/56864f5beee072ae8d0ae91c69e6727455e89552/Screenshot%202025-12-09%20131335.png)
##### Port default/80
  ![alt](https://github.com/Maleka0809/FP_JARKOM/blob/56864f5beee072ae8d0ae91c69e6727455e89552/Screenshot%202025-12-09%20131350.png)

- Explanation
Slav dikonfigurasi untuk listen secara eksklusif pada port 8000 dan 8888. Dengan tidak adanya listen 80, web server hanya akan merespons permintaan yang ditujukan ke port-port kustom tersebut, meningkatkan segmentasi layanan.

##### Slav (Nginx Server Block)
```
server {
    // SOAL 9: Listen hanya di port kustom
    listen 8000;
    listen 8888;
    server_name parkov.com;
    
    root /myscripts/myweb/slav; 
    index slav.html;
}
```

<br>

## Soal 10

> Untuk memudahkan akses, buatlah satu domain lagi dengan nama **openings.com** yang mengarah ke **Petrov.** Lalu, konfigurasikan juga **Petrov** sebagai **Reverse Proxy** yang akan melakukan forward request ke server yang sesuai berdasarkan URL profile yang diminta oleh klien dengan ketentuan sebagai berikut:
> - Request untuk “openings.com/**sicilian**” harus dialihkan ke web server **Sicilian.**
> - Request untuk “openings.com/**slav**” harus dialihkan ke web server **Slav.**

> _To facilitate access, create another domain with the name **openings.com** that points to **Petrov.** Then, configure **Petrov** as a **Reverse Proxy** that will forward requests to the appropriate server based on the profile URL requested by the client with the following conditions:_
> - _Requests for “openings.com/**sicilian**” must be forwarded to web server **Sicilian.**_
> - _Request for “openings.com/**slav**” must be forwarded to web server **Slav.**_

**Answer:**

- Screenshot

  `Put your screenshot in here`

- Explanation

  Petrov berfungsi sebagai Reverse Proxy menggunakan blok location untuk menangkap URI yang diminta klien dan proxy_pass untuk meneruskan trafik ke backend (Sicilian di port 80 dan Slav di port 8000).

  ##### Petrov (Nginx Server Block)

```
server {
    listen 80;
    server_name openings.com;

    // SOAL 10: Proxy ke Sicilian (10.58.42.2:80)
    location /sicilian {
        proxy_pass http://10.58.42.2/;
    }

    // SOAL 10: Proxy ke Slav (10.58.41.2:8000)
    location /slav {
        proxy_pass http://10.58.41.2:8000/;
    }
    // ...
}
```

<br>

## Soal 11

> Tambahkan juga konfigurasi agar request untuk “openings.com/**random**” akan mengalihkan request ke webserver **Sicilian** dan **Slav** dengan algoritma _round-robin_.

> _Additionally, configure requests for "openings.com/**random**" to be redirected to the **Sicilian** and **Slav** web servers using a round-robin algorithm._

**Answer:**

- Screenshot

  `Put your screenshot in here`

- Explanation

Load Balancing diimplementasikan dengan mendefinisikan blok upstream yang membuat pool server. Algoritma Round-Robin (pemilihan server secara bergantian) adalah algoritma default Nginx untuk distribusi beban.

##### Petrov (Nginx Upstream & Location)

```
// SOAL 11: Definisi Grup Server (Di luar blok server)
upstream backend_servers {
    server 10.58.42.2:80;      // Sicilian
    server 10.58.41.2:8000;    // Slav (Menggunakan port kustom)
}

server {
    listen 80;
    server_name openings.com;

    // SOAL 11: Penggunaan Load Balancer Round-Robin
    location /random {
        proxy_pass http://backend_servers;
    }
    // ...
}

```

<br>

## Soal 12

> Anatoly Parkov berencana untuk melakukan ekspansi secara besar-besaran. Maka dari itu, hapus seluruh konfigurasi Static Routing dan ubah agar seluruh router menggunakan Dynamic Routing. Gunakan protokol RIP!

> _Anatoly Parkov plans to perform a great expansion. Therefore, remove all Static Routing configurations and configure all routers to use Dynamic Routing. Use the RIP protocol!_

**Answer:**

- Screenshot
![alt](https://github.com/Maleka0809/jarkom_praktikum_4/blob/f5035864590c687862a83ef2d35a3c1adf153ed4/Screenshot%202025-12-11%20222812.png)
![alt](https://github.com/Maleka0809/jarkom_praktikum_4/blob/f5035864590c687862a83ef2d35a3c1adf153ed4/Screenshot%202025-12-11%20222838.png)


- Explanation

  untuk no.12 sampai 15 harus start semua router selain smith-morra`/usr/lib/frr/frrinit.sh start`

Konfigurasi dilakukan pada file `/etc/frr/frr.conf` di setiap router (Smith-Morra, Fianchetto, Lucena, dll) menggunakan FRR (Free Range Routing).
```
# Mengaktifkan protokol RIP versi 2
router rip
 version 2
 network 10.0.0.0/8
 redistribute connected
 redistribute static
 redistribute kernel
```
Flag R menandakan rute tersebut dipelajari secara otomatis melalui protokol RIP, bukan di-setting manual (Static).
Penjelasan Cara Kerja

Inisialisasi: Saat layanan FRR aktif, router mengaktifkan protokol RIPv2 pada interface yang terhubung ke jaringan 10.0.0.0/8.

Pertukaran Informasi : Router Smith-Morra "memberitahu" tetangganya (Fianchetto) tentang jaringan yang dimilikinya (Client Budapest). Fianchetto meneruskan informasi ini ke router berikutnya (Lucena).

Update Tabel: Router di ujung lain (Lucena) menerima informasi tersebut dan otomatis memperbarui tabel routing-nya.

Hasil: Terbentuk jalur komunikasi ujung-ke-ujung (End-to-End) secara otomatis. Jika salah satu kabel putus, RIP akan mencoba mencari jalan lain (jika ada) tanpa perlu konfigurasi ulang oleh admin.

<br>

## Soal 13

> Untuk meningkatkan keamanan, konfigurasikan firewall **Smith-Morra** untuk melakukan pembatasan koneksi SSH ke server DNS. Drop semua packet SSH yang berasal dari seluruh client yang memiliki tujuan ke **Caro-Kann** atau **Alekhine.**

> _To increase security, configure the **Smith-Morra** firewall to restrict SSH connections to the **DNS server.** Drop all SSH packets from all clients destined for **Caro-Kann** or **Alekhine.**_

**Answer:**

- Screenshot

![alt](https://github.com/Maleka0809/jarkom_praktikum_4/blob/65fad8e356d6414e0da2d0bb625c7dc15cb5bc8a/Screenshot%202025-12-11%20223045.png)

- Explanation

  ```
  iptables -A FORWARD -p tcp --dport 22 -d 10.58.42.195 -j DROP
  ```
  Penjelasan Cara Kerja
Inspeksi Paket: Saat Client Budapest mencoba melakukan remote access (SSH), paket data dikirim menuju IP DNS Server Caro-Kann.

Filter Firewall: Paket tersebut melewati router Smith-Morra. Firewall memeriksa header paket:

Apakah protokol TCP? Ya.

Apakah tujuannya Port 22? Ya.

Apakah tujuannya IP Caro-Kann? Ya.

Aksi DROP: Karena cocok dengan kriteria aturan blokir, firewall mengeksekusi target DROP. Paket tersebut langsung dihapus dari memori router secara diam-diam.

<br>

## Soal 14

> Nampaknya, web server juga manusia sehingga hanya ingin bekerja di hari kerja. Maka dari itu, semua client hanya bisa mengakses **Sicilian** dan **Slav** pada hari Senin-Jumat pada pukul 09:00-17:00.

> _Apparently, web servers are humans too, so they only want to work on weekdays. Therefore, all clients can only access **Sicilian** and **Slav** on Monday through Friday, 9:00 AM to 5:00 PM._

**Answer:**

- Screenshot

	![alt](https://github.com/Maleka0809/jarkom_praktikum_4/blob/1dfe27b34f96e053f1bff5e499ca25eae92e08bc/Screenshot%202025-12-11%20223221.png)
	<br>
	![alt](https://github.com/Maleka0809/jarkom_praktikum_4/blob/b838c913432025ea0ac8b2f7632a787f2547175a/Screenshot%202025-12-11%20223414.png)
	<br>
	![alt](https://github.com/Maleka0809/jarkom_praktikum_4/blob/760d2788757cfcd777db135ebb069abd19baaab9/Screenshot%202025-12-11%20223525.png)
	<br>
	![alt](https://github.com/Maleka0809/jarkom_praktikum_4/blob/e96edaed821ca13d3c4a227da1f44b67a1f45720/Screenshot%202025-12-11%20223744.png)
	
- Explanation

```
  # 1. Izinkan (ACCEPT) hanya pada Jam Kerja (Senin-Jumat, 09.00-17.00)
iptables -A FORWARD -d 10.58.42.2 -p tcp --dport 80 -m time --timestart 09:00 --timestop 17:00 --weekdays Mon,Tue,Wed,Thu,Fri -j ACCEPT

# 2. Buang (DROP) sisanya (Malam hari/Libur)
iptables -A FORWARD -d 10.58.42.2 -p tcp --dport 80 -j DROP
```
Penjelasan Cara Kerja
Sinkronisasi Waktu: Firewall membaca waktu sistem (system clock) pada router Smith-Morra saat paket lewat.

Logika Seleksi:

Jika waktu saat itu masuk dalam rentang 09:00 - 17:00 dan hari Mon-Fri, paket cocok dengan aturan pertama (ACCEPT). Paket diteruskan.

Jika waktu di luar rentang tersebut (misal jam 20:00), paket tidak cocok dengan aturan pertama, lalu jatuh ke aturan kedua (DROP).

Tujuan: Efisiensi penggunaan bandwidth kantor dan memastikan karyawan fokus bekerja pada jam kerja.

<br>

## Soal 15

> Terakhir, Gerry Paskarov berpesan untuk selalu melakukan logging, sehingga konfigurasikan fitur logging untuk melakukan log terhadap seluruh paket yang di-DROP pada firewall **Smith-Morra.**
> _Finally, Gerry Paskarov advises to always perform logging, so configure a logging feature to log all packets dropped on the **Smith-Morra** firewall._

**Answer:**

- Screenshot

  ![alt](https://github.com/Maleka0809/jarkom_praktikum_4/blob/4c356ac04c78d09ce59f671aec2ec97ba0fcf5cf/Screenshot%202025-12-11%20224058.png)
  ![alt](https://github.com/Maleka0809/jarkom_praktikum_4/blob/796a5e2fe6a1662a4ff72ec2c287f4767f587783/Screenshot%202025-12-11%20224350.png)
  ![alt](https://github.com/Maleka0809/jarkom_praktikum_4/blob/ee3a32309d3affc4b7332b205d312407a85605f2/Screenshot%202025-12-11%20224453.png)

- Explanation

```
# Catat dulu
iptables -A FORWARD -p tcp --dport 22 -d 10.58.42.195 -j LOG --log-prefix "JARKOM-DROP-SSH-Caro: " --log-level 4

# Baru dibuang
iptables -A FORWARD -p tcp --dport 22 -d 10.58.42.195 -j DROP
```
Penjelasan Cara Kerja
Urutan Proses: `iptables` memproses aturan dari atas ke bawah.

Pencatatan: Saat paket ilegal (SSH) masuk, ia pertama kali mengenai aturan `LOG`. Kernel Linux mencatat detail paket (IP Asal, IP Tujuan, Interface Masuk/Keluar, MAC Address) ke dalam log sistem (`/var/log/kern.log`).

Pemusnahan: Setelah dicatat, paket lanjut ke aturan berikutnya (`DROP`) dan dimusnahkan.

Tujuan: Membantu administrator jaringan melakukan audit keamanan dan mengetahui siapa yang mencoba melakukan akses ilegal, kapan kejadiannya, dan dari mana asalnya.

<br>


  
## Problems


## Revisions (if any)
nomor 8, 9, 10, 12, 13, 14, 15.
