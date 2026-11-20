# 2.2 Operatörler (Aritmetik, Karşılaştırma ve Mantıksal)

Operatörler, değişkenler ve değerler üzerinde matematiksel hesaplama, büyüklük/eşitlik karşılaştırması veya mantıksal birleştirme yapmamızı sağlayan sembollerdir.

---

## 1. Aritmetik Operatörler (`+`, `-`, `*`, `/`, `%`, `//`, `**`)

Sayısal veriler (`int` ve `float`) üzerinde dört işlem ve mod alma gibi matematiksel hesaplamalar için kullanılır.

| Operatör | İşlem Adı | Örnek | Sonuç | Açıklama |
| :---: | :--- | :---: | :---: | :--- |
| `+` | Toplama | `15 + 4` | `19` | İki sayıyı toplar (String'leri ise uç uca birleştirir) |
| `-` | Çıkarma | `15 - 4` | `11` | Sağdaki sayıyı soldakinden çıkarır |
| `*` | Çarpma | `15 * 4` | `60` | İki sayıyı çarpar |
| `/` | Bölme | `15 / 4` | `3.75` | Her zaman `float` (ondalıklı) sonuç döndürür |
| `%` | Mod Alma (Kalan) | `15 % 4` | `3` | Bölme işleminden kalanı verir (çift/tek kontrolünde sık kullanılır) |
| `//` | Tam Bölme | `15 // 4` | `3` | Bölme sonucunun tam kısmını verir |
| `**` | Üs Alma | `2 ** 3` | `8` | Sayının kuvvetini alır ($2^3 = 8$) |

```python
# Otonom araç ortalama hız ve batarya tüketimi hesabı
toplam_yol_m = 1250
sure_sn = 100

ortalama_hiz = toplam_yol_m / sure_sn       # 12.5 m/s (float)
tam_tur_sayisi = toplam_yol_m // 400        # 400m pistte 3 tam tur
kalan_mesafe = toplam_yol_m % 400           # Son turda gidilen 50 metre

print(f"Hız: {ortalama_hiz} m/s | Tam Tur: {tam_tur_sayisi} | Kalan: {kalan_mesafe} m")
```

---

## 2. Karşılaştırma Operatörler (`==`, `!=`, `>`, `<`, `>=`, `<=`)

İki değeri karşılaştırır ve sonuç olarak her zaman **`True` (Doğru)** veya **`False` (Yanlış)** (`bool`) döndürür.

| Operatör | Anlamı | Örnek (`hiz = 50`) | Sonuç |
| :---: | :--- | :---: | :---: |
| `==` | Eşit mi? | `hiz == 50` | `True` |
| `!=` | Eşit değil mi? (Farklı mı?) | `hiz != 50` | `False` |
| `>` | Büyük mü? | `hiz > 30` | `True` |
| `<` | Küçük mü? | `hiz < 30` | `False` |
| `>=` | Büyük veya eşit mi? | `hiz >= 50` | `True` |
| `<=` | Küçük veya eşit mi? | `hiz <= 40` | `False` |

> **Dikkat:** Tek eşittir (`=`) **değer atama** operatörüdür; çift eşittir (`==`) ise **eşitlik kontrolü** operatörüdür.

---

## 3. Mantıksal Operatörler (`and`, `or`, `not`)

Birden fazla koşulu birleştirmek veya bir koşulun tersini almak için kullanılır.

1. **`and` (VE):** Bağlanan **tüm koşullar `True`** ise `True`, en az biri `False` ise `False` döner.
2. **`or` (VEYA):** Bağlanan koşullardan **en az biri `True`** ise `True`, hepsi `False` ise `False` döner.
3. **`not` (DEĞİL):** Koşulun mantıksal tersini alır (`not True` → `False`, `not False` → `True`).

```python
batarya_yuzdesi = 75
sensorler_aktif = True
acil_durum_butonu = False

# Aracın harekete geçebilmesi için batarya %20'den büyük OLMALI VE sensörler aktif OLMALI VE acil durum olmamalı
hareket_izni = (batarya_yuzdesi > 20) and sensorler_aktif and (not acil_durum_butonu)
print("Otonom Sürüş Başlatılabilir mi?:", hareket_izni)  # True
```
