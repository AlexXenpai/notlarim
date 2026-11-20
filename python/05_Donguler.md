# 2.5 Döngüler (`for`, `while`, `break` – `continue` ve Liste Döngüleri)

Döngüler, belirli bir kod bloğunu bir koşul sağlandığı sürece veya bir veri koleksiyonunun (liste, tuple, string vb.) her elemanı için **tekrarlı olarak çalıştırmamızı** sağlayan yapılardır.

---

## 1. `for` Döngüsü
Tekrar sayısı belli olan durumlarda veya bir dizinin elemanları üzerinde sırayla gezinmek (iterasyon) için kullanılır.

```python
# range(başlangıç, bitiş, adım) kullanımı (bitiş dahil değildir)
for saniye in range(1, 6):
    print(f"Kalibrasyon adımı: {saniye}. saniye")
```

### Listeler Üzerinde `for` Döngüsü Kullanımı
```python
sensor_listesi = ["Kamera", "3D LiDAR", "mmWave Radar", "IMU", "RTK-GPS"]

# 1. Doğrudan elemanlar üzerinde gezinme
for sensor in sensor_listesi:
    print(f"[AKTİF] {sensor} bağlantısı doğrulandı.")

# 2. enumerate() ile hem sıra numarası (indeks) hem elemanı alma
for sira, sensor in enumerate(sensor_listesi, start=1):
    print(f"{sira}. Sensör: {sensor}")
```

---

## 2. `while` Döngüsü
Tekrar sayısının baştan bilinmediği, **belirli bir koşul `True` olduğu sürece** çalışmaya devam etmesi gereken durumlarda kullanılır *(Örn: Kullanıcı 'Çıkış' seçeneğini girene kadar menüyü göstermek veya araç hedefe varana kadar sensör okumak)*.

```python
batarya = 100

while batarya > 20:
    print(f"Otonom devriye devam ediyor... (Batarya: %{batarya})")
    batarya -= 25  # Her turda %25 azalır (sonsuz döngüyü önlemek için sayaç güncellenmeli!)

print(f"Batarya kritik seviyede (%{batarya})! Şarj istasyonuna dönülüyor.")
```

---

## 3. `break` ve `continue` İfadeleri

- **`break`:** Döngüyü **anında ve tamamen sonlandırır**, döngü bloğunun dışına çıkar *(Örn: Aranan eleman bulunduğunda veya acil durdurma sinyali geldiğinde)*.
- **`continue`:** Döngüyü tamamen kırmaz; yalnızca **o anki adımı (turu) atlayıp** döngünün bir sonraki adımına geçer *(Örn: Hatalı/negatif sensör ölçümünü filtreleyip sıradaki ölçüme geçmek)*.

```python
lidar_olcumleri = [12.5, 8.2, -1.0, 5.4, 0.8, 15.0]  # -1.0 hatalı ölçüm, <1.0 kritik engel

for mesafe in lidar_olcumleri:
    if mesafe < 0:
        print("Hatalı ölçüm (-1.0) algılandı, bu veri atlanıyor (continue)...")
        continue

    if mesafe < 1.0:
        print(f"KRİTİK ENGEL ({mesafe} m)! Sürüş döngüsü durduruldu (break)!")
        break

    print(f"Güvenli mesafe ölçümü işlendi: {mesafe} m")
```
