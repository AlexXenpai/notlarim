# 2.1 Değişkenler ve Veri Tipleri

## 1. Değişken (Variable) Nedir?
Değişkenler, program içerisinde verileri bellekte (RAM) geçici olarak saklamamızı ve bu verilere bir isim üzerinden tekrar ulaşmamızı sağlayan etiketlerdir. Python'da değişken tanımlarken veri tipini önceden belirtmek gerekmez (**Dinamik Tiplendirme / Dynamic Typing**).

```python
arac_adi = "TALOS-1"
hiz_kmh = 45
batarya_voltaji = 48.6
otonom_mod_aktif = True
```

### Değişken İsimlendirme Kuralları (PEP 8)
- Sayı ile başlayamaz (`1_sensor` hatalıdır, `sensor_1` doğrudur).
- Boşluk ve özel karakter (`-`, `/`, `*`) içeremez; kelimeler alt çizgi (`_`) ile ayrılır (**snake_case**).
- Python anahtar kelimeleri (`if`, `for`, `class`, `def`, `return`) değişken adı olamaz.

---

## 2. Temel Veri Tipleri (`int`, `float`, `str`, `bool`)

| Veri Tipi | Python İfadesi | Açıklama | Örnek Değer |
| :--- | :---: | :--- | :--- |
| **Tam Sayı (Integer)** | `int` | Pozitif, negatif veya sıfır tam sayılar | `42`, `-10`, `0`, `120` |
| **Ondalıklı Sayı (Float)** | `float` | Nokta (`.`) ile ayrılan kesirli/ondalıklı sayılar | `3.14`, `12.75`, `-0.5` |
| **Metin (String)** | `str` | Tek (`' '`) veya çift (`" "`) tırnak içindeki karakter dizileri | `"TALOS"`, `'Bursa'` |
| **Mantıksal (Boolean)** | `bool` | Yalnızca doğru (`True`) veya yanlış (`False`) değerini alır | `True`, `False` |

```python
tekerlek_sayisi = 4              # int
engel_mesafesi = 14.85           # float
aktif_sensor = "3D LiDAR"        # str
acil_fren_durumu = False         # bool
```

---

## 3. `type()` Fonksiyonu Kullanımı
Bir değişkenin veya değerin bellekte hangi veri tipinde tutulduğunu öğrenmek için `type()` yerleşik fonksiyonu kullanılır.

```python
hiz = 60
mesafe = 18.4
plaka = "16 TALOS 01"
sistem_hazir = True

print(type(hiz))           # Çıktı: <class 'int'>
print(type(mesafe))        # Çıktı: <class 'float'>
print(type(plaka))         # Çıktı: <class 'str'>
print(type(sistem_hazir))  # Çıktı: <class 'bool'>
```

---

## 4. `input()` ile Kullanıcıdan Veri Alma ve Tip Dönüşümü (Type Casting)
`input()` fonksiyonu terminal üzerinden kullanıcıdan veri almamızı sağlar.

> **Çok Önemli Kural:** `input()` fonksiyonu, kullanıcı sayı bile girse aldığı veriyi **her zaman `str` (string)** tipinde döndürür. Matematiksel işlem yapılacaksa `int()` veya `float()` ile tip dönüşümü yapılmalıdır.

```python
# Kullanıcıdan string alma
pilot_adi = input("Operatör adınızı giriniz: ")

# Kullanıcıdan sayısal veri alma (int ve float dönüşümü)
hedef_hiz = int(input("Hedef hızı giriniz (km/s): "))
guvenli_mesafe = float(input("Güvenli takip mesafesini giriniz (metre): "))

print(f"Operatör: {pilot_adi} | Hedef Hız: {hedef_hiz} km/s | Mesafe: {guvenli_mesafe} m")
print("hedef_hiz tipi:", type(hedef_hiz))  # <class 'int'>
```
