# 2.3 Koşul Yapıları (`if`, `elif`, `else` ve İç İçe Koşullar)

Programların sabit bir sırayla çalışmak yerine, gelen verilere göre **karar vermesini ve farklı yollara dallanmasını** sağlayan yapılara koşul yapıları denir.

---

## 1. `if`, `elif`, `else` Temel Yapısı

- **`if` (Eğer):** İlk kontrol edilen koşuldur. Koşul `True` ise altındaki girintili (4 boşluk) blok çalışır.
- **`elif` (Değilse Eğer):** Üstteki `if` (veya önceki `elif`) yanlışsa kontrol edilen alternatif koşuldur. İstenildiği kadar `elif` eklenebilir.
- **`else` (Hiçbiri Değilse):** Yukarıdaki koşulların tamamı `False` olduğunda çalışan varsayılan bloktur.

```python
engel_mesafesi = float(input("LiDAR engel mesafesi (metre): "))

if engel_mesafesi <= 3.0:
    print("KRİTİK TEHLİKE: Acil fren uygulanıyor! (Hız = 0 km/s)")
elif engel_mesafesi <= 10.0:
    print("UYARI: Yavaşlanıyor, güvenli takip mesafesine çekiliyor.")
else:
    print("YOL AÇIK: Normal seyir hızında devam ediliyor.")
```

---

## 2. İç İçe Koşullar (Nested `if`)

Bir koşul sağlandıktan sonra, o durumun kendi içinde ikinci bir doğrulama veya alt karara ihtiyaç duyması halinde **`if` içinde `if`** (iç içe koşul) kullanılır.

```python
otonom_mod = True
trafik_isigi = "kirmizi"
yaya_gecidi_bos = False

if otonom_mod:
    print("Otonom sürüş denetimi aktif.")
    if trafik_isigi == "kirmizi":
        print("Kırmızı ışık algılandı: Araç durduruluyor.")
    elif trafik_isigi == "yesil":
        if yaya_gecidi_bos:
            print("Yeşil ışık ve yaya geçidi boş: Geçiş yapılıyor.")
        else:
            print("Yeşil ışık yanıyor ANCAK yaya geçidinde yaya var! Bekleniyor.")
else:
    print("Manuel sürüş modu: Kontrol sürücüde.")
```

---

## 3. Gerçek Hayat Örnekleri

### Örnek 1: Yetki ve Sistem Erişim Kontrolü
```python
kullanici_adi = input("Kullanıcı adı: ")
rol = input("Rolünüz (admin / operator / misafir): ")
aktif_hesap = True

if aktif_hesap:
    if rol == "admin" and kullanici_adi == "talos_kaptan":
        print("Tam Yetki: Araç parametrelerini değiştirebilir ve sürüş başlatabilirsiniz.")
    elif rol == "operator":
        print("Operatör Yetkisi: Telemetri izleyebilir ve simülasyon çalıştırabilirsiniz.")
    else:
        print("Sınırlı Yetki: Yalnızca salt-okunur (read-only) log kayıtlarını görebilirsiniz.")
else:
    print("HATA: Hesabınız askıya alınmış, erişim reddedildi!")
```

### Örnek 2: Banka Hesap ve Bakiye Denetimi
```python
bakiye = 2500.0
gunluk_limit = 2000.0
cekilecek_tutar = float(input("Çekmek istediğiniz tutar (TL): "))

if cekilecek_tutar <= 0:
    print("Hata: Geçersiz tutar girdiniz!")
elif cekilecek_tutar > bakiye:
    print(f"Yetersiz bakiye! Mevcut bakiyeniz: {bakiye} TL")
elif cekilecek_tutar > gunluk_limit:
    print(f"Günlük çekim limitini ({gunluk_limit} TL) aştınız!")
else:
    bakiye -= cekilecek_tutar
    print(f"İşlem başarılı! Kalan bakiyeniz: {bakiye} TL")
```
