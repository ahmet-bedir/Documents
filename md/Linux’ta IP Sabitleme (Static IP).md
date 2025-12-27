# Linux’ta IP Sabitleme (Static IP)

## 1. IP Sabitleme Nedir?

IP sabitleme, bir ağ arayüzüne **manuel olarak belirlenen IP adresinin** atanmasıdır.
 DHCP ile otomatik IP almak yerine sistem her açılışta **aynı IP adresini** kullanır.

------

## 2. Neden IP Sabitlenir?

- Sunucu ve servis erişimleri (SSH, Web, DB) kararlı olur
- Port yönlendirme sorunsuz çalışır
- Firewall ve güvenlik kuralları tutarlı olur
- Ağ yönetimi ve log takibi kolaylaşır

------

## 3. Gerekli Bilgiler

IP sabitlemeden önce aşağıdaki bilgiler bilinmelidir:

- **IP Adresi** → `192.168.1.50`
- **Subnet / Prefix** → `/24` (255.255.255.0)
- **Gateway** → `192.168.1.1`
- **DNS Sunucuları** → `1.1.1.1`, `8.8.8.8`
- **Ağ Arayüzü** → `eth0`, `enp0s3`, `wlan0`

------

## 4. NetworkManager (Masaüstü Sistemler)

### Mantık

- DHCP kapatılır
- IPv4 yöntemi **Manual** yapılır
- IP, Gateway ve DNS elle girilir

### Komut Satırı (nmcli)

```

nmcli con show
nmcli con mod "Wired connection 1" \
  ipv4.method manual \
  ipv4.addresses 192.168.1.50/24 \
  ipv4.gateway 192.168.1.1 \
  ipv4.dns "1.1.1.1 8.8.8.8"

nmcli con up "Wired connection 1"
```

------

## 5. Netplan (Ubuntu / Kali)

### Dosya Konumu

```

/etc/netplan/*.yaml
```

### Örnek Yapılandırma

```

network:
  version: 2
  renderer: networkd
  ethernets:
    eth0:
      dhcp4: no
      addresses:
        - 192.168.1.50/24
      gateway4: 192.168.1.1
      nameservers:
        addresses:
          - 1.1.1.1
          - 8.8.8.8
```

### Uygulama

```

sudo netplan apply
```

------

## 6. systemd-networkd (Sunucu Sistemleri)

### Yapılandırma Dosyası

```

/etc/systemd/network/20-eth0.network

[Match]
Name=eth0

[Network]
Address=192.168.1.50/24
Gateway=192.168.1.1
DNS=1.1.1.1
DNS=8.8.8.8

sudo systemctl restart systemd-networkd
```

------

## 7. Eski Yöntem: `/etc/network/interfaces`

> Yeni dağıtımlarda **önerilmez**.

```

auto eth0
iface eth0 inet static
    address 192.168.1.50
    netmask 255.255.255.0
    gateway 192.168.1.1
    dns-nameservers 1.1.1.1 8.8.8.8
```

------

## 8. Router Üzerinden IP Sabitleme (DHCP Reservation)

- Linux tarafında ayar yapılmaz
- Router, MAC adresine her zaman aynı IP’yi verir
- IP çakışması riski yoktur

**En temiz ve güvenli yöntemdir.**

------

## 9. Kontrol Komutları

```

ip a
ip route
resolvectl status
```

------

## 10. Hangi Yöntem Ne Zaman?

| Senaryo       | Önerilen         |
| ------------- | ---------------- |
| GNOME / KDE   | NetworkManager   |
| Kali / Ubuntu | Netplan          |
| Sunucu        | systemd-networkd |
| Ev / Ofis Ağı | DHCP Reservation |

​	