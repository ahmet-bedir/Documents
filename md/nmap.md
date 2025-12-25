## 1. Yerel makinenizi taramak için temel komut

```

sudo nmap -sTU -p- localhost
```

Açıklama:

- `-sT` = TCP connect taraması (root yetkisi gerekmez ama yavaştır)
- `-sU` = UDP taraması
- `-sTU` = hem TCP hem UDP
- `-p-` = tüm portları tara (1–65535)
- `localhost` veya `127.0.0.1` = kendi makinenizi tarar

------

## 2. Sadece TCP portlarını görmek isterseniz

```

sudo nmap -sS -p- localhost
```

- `-sS` = SYN scan (hızlı ve en doğru sonuç, root gerektirir)

------

## 3. En sık kullanılan portların hızlı taraması

```

nmap localhost
```

Bu komut yalnızca en popüler ~1000 portu tarar.

------

## 4. Servis versiyonlarını da görmek isterseniz

```

sudo nmap -sV localhost
```

Açık portlarda hangi servis ve versiyon çalışıyor gösterir.

------

## 5. Firewall engelliyor mu görmek için

```

sudo nmap -Pn localhost
```

------

### Önemli Not

Kendi makineni taramak tamamen güvenlidir; **nmap sadece dinleyen portları listeler** ve sistemde değişiklik yapmaz.