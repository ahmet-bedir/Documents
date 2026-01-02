## Önerilen Kullanıcılar Tablosu

```

CREATE TABLE kullanicilar (
    id INTEGER GENERATED ALWAYS AS IDENTITY PRIMARY KEY,
    ad VARCHAR(50) NOT NULL,
    soyad VARCHAR(50) NOT NULL,
    kullanici_adi VARCHAR(50) UNIQUE NOT NULL,
    e_posta VARCHAR(100) UNIQUE NOT NULL,
    sifre TEXT NOT NULL,
    telefon VARCHAR(20),
    dogum_tarihi DATE,
    aktif BOOLEAN DEFAULT true,
    kayit_tarihi TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);
```

------

## Kolonların Açıklaması

| Kolon           | Açıklama                          |
| --------------- | --------------------------------- |
| `id`            | Birincil anahtar (otomatik artan) |
| `ad`            | Kullanıcının adı                  |
| `soyad`         | Kullanıcının soyadı               |
| `kullanici_adi` | Sistemde benzersiz kullanıcı adı  |
| `e_posta`       | E-posta adresi (benzersiz)        |
| `sifre`         | Şifre (hashlenmiş olmalı)         |
| `telefon`       | Telefon numarası                  |
| `dogum_tarihi`  | Doğum tarihi                      |
| `aktif`         | Kullanıcı aktif mi                |
| `kayit_tarihi`  | Sisteme kayıt zamanı              |

------

## Örnek INSERT

```

INSERT INTO kullanicilar (ad, soyad, kullanici_adi, e_posta, sifre)
VALUES ('Ahmet', 'Bedir', 'ahmetb', 'ahmet@mail.com', 'hashli_sifre');
```

------

## Türkçe Karakterle Yazmak İstersen (Alternatif)

PostgreSQL bunu kabul eder, **ama önerilmez**:

```

CREATE TABLE "kullanıcılar" (
    "id" SERIAL PRIMARY KEY,
    "ad" TEXT,
    "şifre" TEXT
);
```

Bu durumda **her sorguda çift tırnak kullanmak zorunda kalırsın**:

```

SELECT "şifre" FROM "kullanıcılar";
```

------

## Profesyonel Tavsiye

- Kolon adları: **Türkçe ama ASCII**
- Tablo adları: **küçük harf**
- Şifre: **asla düz metin saklama**
- `PRIMARY KEY + UNIQUE` mutlaka tanımla

------

İstersen:

- **foreign key’li rol tablosu**
- **login / audit log tasarımı**
- **index önerileri**

üzerinden devam edebiliriz.

bu tablo için 1000 den fazla kayıt csv

İstediğiniz tablo yapısına uygun **1200 adet kayıt içeren CSV dosyasını** oluşturdum.

**Dosya:**
 CSV dosyasını indir – kullanicilar_1200_kayit.csv

------

## CSV İçeriği (Kolonlar)

Dosya, daha önce oluşturduğumuz tabloyla **birebir uyumludur**:

```

ad, soyad, kullanici_adi, e_posta, sifre, telefon,
dogum_tarihi, aktif, kayit_tarihi
```

- `id` kolonu **bilinçli olarak yok**
   → PostgreSQL `IDENTITY / SERIAL` otomatik üretecek
- Türkçe isimler
- UNIQUE alanlar (`kullanici_adi`, `e_posta`) çakışmaz
- `BOOLEAN`, `DATE`, `TIMESTAMP` uyumlu

------

## PostgreSQL’e CSV Import (Önerilen)

### 1. Sunucu Tarafında (COPY)

```

COPY kullanicilar (
    ad, soyad, kullanici_adi, e_posta, sifre,
    telefon, dogum_tarihi, aktif, kayit_tarihi
)
FROM '/path/kullanicilar_1200_kayit.csv'
DELIMITER ','
CSV HEADER;
```

### 2. Client Tarafında (psql → \copy)

```

\copy kullanicilar (
    ad, soyad, kullanici_adi, e_posta, sifre,
    telefon, dogum_tarihi, aktif, kayit_tarihi
)
FROM 'kullanicilar_1200_kayit.csv'
CSV HEADER;
```

------

## DBeaver ile Import

1. Tabloya sağ tık → **Import Data**
2. CSV seç
3. Kolon eşleşmelerini kontrol et
4. `id` kolonunu **skip** et
5. Finish