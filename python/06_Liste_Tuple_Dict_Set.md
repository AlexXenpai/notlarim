# 2.6 Veri Yapıları: Liste (`list`), Demet (`tuple`), Sözlük (`dict`), Küme (`set`)

Python'da birden fazla veriyi bir arada tutmak için kullanılan 4 temel koleksiyon veri yapısı vardır:

| Veri Yapısı | Gösterim | Sıralı mı? (İndeksli) | Değiştirilebilir mi? (Mutable) | Tekrarlı Eleman İzinli mi? |
| :--- | :---: | :---: | :---: | :---: |
| **Liste (`list`)** | `[ ]` | ✅ Evet | ✅ Evet | ✅ Evet |
| **Tuple (`tuple`)** | `( )` | ✅ Evet | ❌ Hayır (Immutable) | ✅ Evet |
| **Sözlük (`dict`)** | `{k: v}` | ✅ Evet (Ekleme sırası) | ✅ Evet | ❌ Anahtarlar (key) benzersizdir |
| **Küme (`set`)** | `{ }` | ❌ Hayır | ✅ Evet | ❌ Hayır (Her eleman tektir) |

---

## 1. Liste (`list`) — Temel Kullanım ve En Çok Kullanılan Fonksiyonlar
Sıralı, indekslenebilir (`0`'dan başlar) ve sonradan eleman eklenip silinebilen en esnek veri yapısıdır.

```python
gorevler = ["Sensör kontrolü", "Harita yükleme", "Rota planlama"]

# En çok kullanılan liste metotları:
gorevler.append("Sürüş başlat")          # Sona eleman ekler
gorevler.insert(1, "Kamera kalibrasyon") # Belirtilen indekse eleman ekler
gorevler.remove("Harita yükleme")        # Değere göre elemanı siler
son_gorev = gorevler.pop()               # Sondaki elemanı siler ve döndürür
gorevler.sort()                          # Listeyi alfabetik / küçükten büyüğe sıralar
print("Görev sayısı:", len(gorevler))    # len() eleman sayısını verir
```

---

## 2. Demet (`tuple`) — Değiştirilemez Sıralı Veriler
Oluşturulduktan sonra elemanları **değiştirilemeyen (`immutable`)** veri yapısıdır. Sabit kalması gereken koordinatlar, kamera çözünürlüğü veya yapılandırma sabitleri için kullanılır.

```python
baslangic_koordinati = (40.2254, 28.8742)  # Bursa Uludağ Üniversitesi (Enlem, Boylam)
kamera_cozunurluk = (1920, 1080, 1080)

print("Enlem:", baslangic_koordinati[0])
print("1080 değeri kaç kez geçiyor?:", kamera_cozunurluk.count(1080))
print("1920'nin indeksi:", kamera_cozunurluk.index(1920))
```

---

## 3. Sözlük (`dict`) — Anahtar-Değer (`Key-Value`) Çiftleri
Verileri indeks numarası yerine anlamlı **Anahtar (`Key`) : Değer (`Value`)** çiftleri halinde saklar.

```python
arac_telemetri = {
    "model": "TALOS-Otonom",
    "hiz_kmh": 35,
    "batarya": 88.5,
    "aktif": True
}

# En çok kullanılan sözlük metotları:
print(arac_telemetri.get("hiz_kmh", 0))  # Güvenli değer okuma (yoksa 0 döner)
arac_telemetri["hiz_kmh"] = 42           # Değer güncelleme
arac_telemetri["mod"] = "Otonom"         # Yeni anahtar-değer ekleme
arac_telemetri.pop("aktif")              # Anahtarı ve değerini silme

for anahtar, deger in arac_telemetri.items():
    print(f"{anahtar}: {deger}")         # .keys(), .values(), .items()
```

---

## 4. Küme (`set`) — Benzersiz Elemanlar ve Küme İşlemleri
Tekrar eden elemanları otomatik olarak filtreler ve matematiksel küme işlemlerini (kesişim, birleşim, fark) çok hızlı yapar.

```python
kamera_tespitleri = {"Yaya", "Araç", "Trafik Levhası", "Yaya"}  # Tekrarlayan 'Yaya' silinir
lidar_tespitleri = {"Araç", "Bariyer", "Yaya"}

kamera_tespitleri.add("Bisiklet")
ortak_tespitler = kamera_tespitleri.intersection(lidar_tespitleri)  # Kesişim (&)
tum_tespitler = kamera_tespitleri.union(lidar_tespitleri)           # Birleşim (|)

print("Her iki sensörün ortak gördüğü nesneler:", ortak_tespitler)  # {'Yaya', 'Araç'}
```

---

## 5. Mini Uygulama Örneği: Sensör Veri Özeti
```python
ham_loglar = ["LiDAR", "Kamera", "LiDAR", "IMU", "Kamera", "Radar"]
benzersiz_sensorler = set(ham_loglar)  # Set ile tekrarları temizle
sayim_sozlugu = {}                     # Dict ile her sensörün kaç mesaj attığını say

for sensor in benzersiz_sensorler:
    sayim_sozlugu[sensor] = ham_loglar.count(sensor)

print("Sensör Mesaj Sayıları:", sayim_sozlugu)
```
