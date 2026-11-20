# 2.7 Sınıflar (`class`) ve Nesne Tabanlı Programlama (OOP)

## 1. Nesne Tabanlı Programlama (OOP) ve Sınıf (`class`) Nedir?
**Nesne Tabanlı Programlama (Object-Oriented Programming - OOP)**, gerçek dünyadaki varlıkları yazılım dünyasında **özellikleri (attributes)** ve **davranışları/yetkinlikleri (methods)** ile birlikte modelleme yaklaşımıdır.

- **Sınıf (`class`):** Bir nesnenin hangi özelliklere ve metotlara sahip olacağını belirleyen **taslak veya şablondur** *(Örn: `OtonomArac` şablonu veya `Gorev` şablonu)*.
- **Nesne (`object` / `instance`):** Sınıftan üretilen somut örnektir *(Örn: `talos_1 = OtonomArac("TALOS-1", 50)` nesnesi)*.

---

## 2. `class` Oluşturma, `__init__` ve `self` Kullanımı

- **`__init__` (Yapıcı Metot / Constructor):** Sınıftan yeni bir nesne oluşturulduğu anda **otomatik olarak çalışan** ilk metottur. Nesnenin başlangıç özelliklerini (attribute) tanımlamak için kullanılır.
- **`self`:** Sınıf içindeki özelliklerin ve metotların **o an işlem yapılan nesneye ait olduğunu** belirten referanstır. Sınıf içindeki tüm metotların ilk parametresi `self` olmalıdır.

```python
class Sensor:
    def __init__(self, ad, frekans_hz):
        # Nesne özellikleri (Attributes)
        self.ad = ad
        self.frekans_hz = frekans_hz
        self.aktif = False

    # Metot tanımlama (Nesnenin davranışları)
    def baslat(self):
        self.aktif = True
        return f"{self.ad} sensörü ({self.frekans_hz} Hz) başlatıldı."

    def durum_bilgisi(self):
        durum = "Aktif" if self.aktif else "Pasif"
        return f"[{durum}] {self.ad} - {self.frekans_hz} Hz"


# Nesne oluşturma (Instantiation) ve metot çağırma
lidar = Sensor("Velodyne 3D LiDAR", 20)
kamera = Sensor("ZED 2i Stereo Kamera", 60)

print(lidar.baslat())
print(lidar.durum_bilgisi())
print(kamera.durum_bilgisi())
```

---

## 3. Basit Sınıf Temelli Proje Örneği (İki Sınıfın Birlikte Çalışması)

Gerçek projelerde sınıflar birbirleriyle etkileşim kurar. Örneğin bir `Gorev` sınıfı tekil görevi temsil ederken, `GorevYoneticisi` sınıfı bu görev nesnelerinin listesini yönetir:

```python
class Gorev:
    def __init__(self, kod, baslik, oncelik):
        self.kod = kod
        self.baslik = baslik
        self.oncelik = oncelik
        self.tamamlandi = False

    def tamamla(self):
        self.tamamlandi = True


class GorevYoneticisi:
    def __init__(self, ekip_adi):
        self.ekip_adi = ekip_adi
        self.gorev_listesi = []

    def ekle(self, yeni_gorev):
        self.gorev_listesi.append(yeni_gorev)

    def ozet_yazdir(self):
        print(f"--- {self.ekip_adi} Görev Listesi ---")
        for g in self.gorev_listesi:
            ikon = "[✓]" if g.tamamlandi else "[ ]"
            print(f"{ikon} #{g.kod} - {g.baslik} (Öncelik: {g.oncelik})")


# Kullanım:
yonetici = GorevYoneticisi("TALOS Planlama Ekibi")
g1 = Gorev(1, "PID hız kontrol testini tamamla", "Yüksek")
g2 = Gorev(2, "Akış şemasını README dosyasına ekle", "Normal")

yonetici.ekle(g1)
yonetici.ekle(g2)
g1.tamamla()
yonetici.ozet_yazdir()
```
