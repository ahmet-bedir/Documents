<p align="center">
	<img src="../images/network-technology.png" width="415"/>
<p/>

# Linux Ağ Yönetimi

###### Son Güncelleme : 05/2026

**İçindekiler**

- ping



---

## ping

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

