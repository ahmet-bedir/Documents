<p align="center">
	<img src="../images/network-technology.png" width="415"/>
<p/>
## 🖧 Linux Ağ Yönetimi (Network Management)

Linux ağ yönetimi, sistemin ağ arayüzlerini (network interfaces), IP yapılandırmasını, yönlendirme (routing) ve bağlantı servislerini kontrol etme sürecidir. Hem statik hem dinamik (DHCP) ağ yapılandırmaları desteklenir.

**İçindekiler**

- [**ping komutu**](#ping)
- [**ip komutu**](#ip)
- [**nmtui komutu**](#nmtui)



---

## ping komutu

`ping` komutu, ağdaki cihazların erişilebilirliğini ve tepki sürelerini kontrol etmek için kullanılan bir araçtır.

```bash
┌──(ahmet㉿kali)-[~]
└─$ ping www.google.com

PING www.google.com (142.251.156.119) 56(84) bytes of data.
64 bytes from 142.251.156.119: icmp_seq=1 ttl=112 time=39.6 ms
64 bytes from 142.251.156.119: icmp_seq=2 ttl=112 time=38.1 ms
64 bytes from 142.251.156.119: icmp_seq=3 ttl=112 time=38.6 ms
64 bytes from 142.251.156.119: icmp_seq=4 ttl=112 time=35.3 ms
64 bytes from 142.251.156.119: icmp_seq=5 ttl=112 time=36.7 ms
64 bytes from 142.251.156.119: icmp_seq=6 ttl=112 time=33.3 ms
64 bytes from 142.251.156.119: icmp_seq=7 ttl=112 time=37.1 ms
64 bytes from 142.251.156.119: icmp_seq=8 ttl=112 time=35.9 ms
^C
--- www.google.com ping statistics ---
8 packets transmitted, 8 received, 0% packet loss, time 7011ms
rtt min/avg/max/mdev = 33.346/36.841/39.646/1.878 ms
```

Verdiğimiz www.google.com domain adresi çözümlenip “142.251.156.119” ip adresi bulunmuş ve bu adrese küçük bir data paketi gönderilmiş. Göndermiş olduğumuz pakete karşılık olarak da www.google.com adresi 64 byte’lık yanıt paketleri göndermiş.

```bash
┌──(ahmet㉿kali)-[~]
└─$ ping -c 3 www.linuxdersleri.net

PING linux-dersleri.github.io (185.199.108.153) 56(84) bytes of data.
64 bytes from cdn-185-199-108-153.github.com (185.199.108.153): icmp_seq=1 ttl=50 time=94.1 ms
64 bytes from cdn-185-199-108-153.github.com (185.199.108.153): icmp_seq=2 ttl=50 time=70.3 ms
64 bytes from cdn-185-199-108-153.github.com (185.199.108.153): icmp_seq=3 ttl=50 time=60.8 ms

--- linux-dersleri.github.io ping statistics ---
3 packets transmitted, 3 received, 0% packet loss, time 2003ms
rtt min/avg/max/mdev = 60.795/75.069/94.076/13.992 ms
```

Kaç adet paketin gönderileceğini belirtmek için `-c` seçeneği ile sayı belirtmemiz mümkün.

`ping` komutu varsayılan olarak ipv4 adresleri üzerinde çalışıyor. Eğer ipv6 adresleriyle çalışacaksanız `-6` seçeneği ile bunu özellikle belirtmeniz gerekiyor. 

---

## ip komutu

`ip` komutu, ağ arayüzleri hakkında bilgi almak ve yapılandırmak için kullanılır.

Sistemimize bağlı bulunan ağ arayüzleri hakkında bilgi almak için `ip a` ya da `ip addr` ya da uzun şekilde `ip address` şeklinde komutumuzu girebiliriz.

```bash
┌──(ahmet㉿kali)-[~]
└─$ ip a

1: lo: <LOOPBACK,UP,LOWER_UP> mtu 65536 qdisc noqueue state UNKNOWN group default qlen 1000
    link/loopback 00:00:00:00:00:00 brd 00:00:00:00:00:00
    inet 127.0.0.1/8 scope host lo
       valid_lft forever preferred_lft forever
    inet6 ::1/128 scope host noprefixroute 
       valid_lft forever preferred_lft forever
2: eth0: <NO-CARRIER,BROADCAST,MULTICAST,UP> mtu 1500 qdisc fq_codel state DOWN group default qlen 1000
    link/ether 50:a1:32:3c:bf:2d brd ff:ff:ff:ff:ff:ff
3: wlan0: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc noqueue state UP group default qlen 1000
    link/ether c4:3d:1a:bc:34:b9 brd ff:ff:ff:ff:ff:ff
    inet 10.43.239.196/24 brd 10.43.239.255 scope global dynamic noprefixroute wlan0
       valid_lft 2000sec preferred_lft 2000sec
    inet6 fe80::1970:5982:3bc5:7e2a/64 scope link noprefixroute 
       valid_lft forever preferred_lft forever
```

➜ Networke ait genel bilgileri öğrenmek için `ip addr show` komutunu kullanabiliriz.

Eğer ağ arayüzleri tarafından gerçekleştirilen paket transferleri hakkında bilgi edinmek istersek `-s` seçeneğini ekleyebiliriz.

```bash
┌──(ahmet㉿kali)-[~]
└─$ ip -s a

1: lo: <LOOPBACK,UP,LOWER_UP> mtu 65536 qdisc noqueue state UNKNOWN group default qlen 1000
    link/loopback 00:00:00:00:00:00 brd 00:00:00:00:00:00
    inet 127.0.0.1/8 scope host lo
       valid_lft forever preferred_lft forever
    inet6 ::1/128 scope host noprefixroute 
       valid_lft forever preferred_lft forever
    RX:  bytes packets errors dropped  missed   mcast           
         24472     314      0       0       0       0 
    TX:  bytes packets errors dropped carrier collsns           
         24472     314      0       0       0       0 
2: eth0: <NO-CARRIER,BROADCAST,MULTICAST,UP> mtu 1500 qdisc fq_codel state DOWN group default qlen 1000
    link/ether 50:a1:32:3c:bf:2d brd ff:ff:ff:ff:ff:ff
    RX:  bytes packets errors dropped  missed   mcast           
             0       0      0       0       0       0 
    TX:  bytes packets errors dropped carrier collsns           
             0       0      0       0       0       0 
3: wlan0: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc noqueue state UP group default qlen 1000
    link/ether c4:3d:1a:bc:34:b9 brd ff:ff:ff:ff:ff:ff
    inet 10.43.239.196/24 brd 10.43.239.255 scope global dynamic noprefixroute wlan0
       valid_lft 1882sec preferred_lft 1882sec
    inet6 fe80::1970:5982:3bc5:7e2a/64 scope link noprefixroute 
       valid_lft forever preferred_lft forever
    RX:  bytes packets errors dropped  missed   mcast           
      17296456   23732      0       0       0       0 
    TX:  bytes packets errors dropped carrier collsns           
       9112521   16490      0       0       0       0 
```

Buradaki çıktılarda yer alan “lo” ifadesi localhost ya da local loopback olarak bilinen ağ arayüzünü temsil ediyor. Bu arayüz, sayesinde mevcut cihazın kendi kendine ağ trafiği oluşturması ve işlemesi mümkün oluyor. Bu sayede örneğin bir websitesi geliştirirken gerçek ağ trafiği olmadan uygulamanın nasıl çalıştığını test edebiliyoruz.

İkinci ağ arayüzü olan “eth0” ise ethernet bağlantısını (kablo ile bağlantı) temsil eden ağ arayüzüdür.

Üçüncü ağ arayüzü Wi-Fi (kablosuz bağlantı) aygıtı “wlan0” olarak görünüyor.

💡 Uyarı: “eth” ve “wlan” ifadeleri arayüz tipini belirtiyorken, bitişik şekilde yazılan sayılar ise kaçıncı ağ arayüzü olduğunu belirtiyor. Örneğin benim sistemimde 3 tane ethernet ağ kartı(network interface card) bağlı olsaydı buradaki çıktılarda “eth0”, “eth1” ve “eth2” şeklinde sırasıyla isimlendirilmiş ethernet arayüzlerini görecektik.

### Ağ Arayüzlerini Açıp Kapatmak | UP DOWN

Üzerinde işlem yapmak istediğimiz arayüzü `ip link set` komutundan sonra yazıp, yapmak istediğimiz işlemi belirtiriz.

Ethernet arayüzünü kapatmak için:

```bash
┌──(ahmet㉿kali)-[~]
└─$ sudo ip link set eth0 down
[sudo] password for ahmet:

┌──(ahmet㉿kali)-[~]
└─$ ip address
1: lo: <LOOPBACK,UP,LOWER_UP> mtu 65536 qdisc noqueue state UNKNOWN group default qlen 1000
    link/loopback 00:00:00:00:00:00 brd 00:00:00:00:00:00
    inet 127.0.0.1/8 scope host lo
       valid_lft forever preferred_lft forever
    inet6 ::1/128 scope host 
       valid_lft forever preferred_lft forever
2: eth0: <BROADCAST,MULTICAST> mtu 1500 qdisc pfifo_fast state DOWN group default qlen 1000
    link/ether 08:00:27:95:bd:54 brd ff:ff:ff:ff:ff:ff
````

Gördüğünüz gibi ethernet bağlantısını temsil eden **eth0** arayüzünün **state** yani durumu **DOWN** olarak gözüküyor.

Şimdi kapatmış olduğumuz ağ arayüzünü tekrar aktifleştirmek üzere bu kez `up` seçeneğini kullanalım.

```bash
┌──(ahmet㉿kali)-[~]
└─$ sudo ip link set eth0 up

┌──(ahmet㉿kali)-[~]
└─$ ip address             
1: lo: <LOOPBACK,UP,LOWER_UP> mtu 65536 qdisc noqueue state UNKNOWN group default qlen 1000
    link/loopback 00:00:00:00:00:00 brd 00:00:00:00:00:00
    inet 127.0.0.1/8 scope host lo
       valid_lft forever preferred_lft forever
    inet6 ::1/128 scope host 
       valid_lft forever preferred_lft forever
2: eth0: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc pfifo_fast state UP group default qlen 1000
    link/ether 08:00:27:95:bd:54 brd ff:ff:ff:ff:ff:ff
    inet 192.168.1.11/24 brd 192.168.1.255 scope global dynamic noprefixroute eth0
       valid_lft 86398sec preferred_lft 86398sec
    inet6 fe80::a00:27ff:fe95:bd54/64 scope link noprefixroute 
       valid_lft forever preferred_lft forever
```
 
Bakın `sudo ip link set eth0 up` komutu sayesinde `eth0` arayüzünü tekrar aktifleştirmiş olduk.
 
 

ethtool -i (network kartı) # Network kartının bilgilerini verir
ethtool -S (network kartı) # Network kartının daha detaylı bilgileri verir

DNS ayarlarının olduğu dosya `/etc/resolv.conf` konumundadır.

Ağda bulunan tüm aygıtları görmek için`netdiscover` komutu kullanılır.