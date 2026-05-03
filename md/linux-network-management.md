<p align="center">
	<img src="../images/network-technology.png" width="415"/>
<p/>

# Linux Ağ Yönetimi

###### Son Güncelleme : 05/2026

**İçindekiler**

- ping



---

## ping Komutu

`ping` komutu, ağdaki cihazların erişilebilirliğini ve tepki sürelerini kontrol etmek için kullanılan bir araçtır.

```bash
┌──(ahmet㉿kali)-[~/Masaüstü/Documents]
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
┌──(ahmet㉿kali)-[~/Masaüstü/Documents]
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

## ip Komutu

`ip` komutu, ağ arayüzleri hakkında bilgi almak ve yapılandırmak için kullanılır.

