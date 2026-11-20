# 2.4 Fonksiyonlar (`def`, Parametreler, `return` ve Modülerlik)

## 1. Fonksiyon Nedir?
Fonksiyonlar, belirli bir görevi yerine getirmek üzere bir kez yazılıp isimlendirilen ve programın istenilen yerinde tekrar tekrar çağrılabilen kod bloklarıdır. Python'da fonksiyonlar **`def`** (define) anahtar kelimesiyle tanımlanır.

```python
def sistem_selamla():
    print("TALOS Otonom Araç Yazılım Sistemi Başlatıldı.")

# Fonksiyonu çağırma
sistem_selamla()
```

---

## 2. Parametreler ve Argümanlar
Fonksiyonların dışarıdan veri alarak dinamik çalışmasını sağlayan değişkenlere **parametre** denir. Ayrıca parametrelere varsayılan değer (default parameter) atanabilir.

```python
def hiz_kontrolu(mevcut_hiz, maksimum_hiz=50):
    if mevcut_hiz > maksimum_hiz:
        print(f"Uyarı! Hızınız ({mevcut_hiz} km/s), limiti ({maksimum_hiz} km/s) aştı!")
    else:
        print(f"Hız normal: {mevcut_hiz} km/s")

hiz_kontrolu(65)          # maksimum_hiz varsayılan olarak 50 alınır
hiz_kontrolu(65, 70)      # maksimum_hiz 70 olarak güncellenir
```

---

## 3. `return` İfadesi
`print()` yalnızca ekrana yazı yazdırır; hesaplanan değeri kodun başka bir yerinde kullanmamızı sağlamaz. **`return`** ifadesi ise fonksiyonun ürettiği sonucu çağrıldığı yere **geri döndürür** ve fonksiyonu sonlandırır.

```python
def fren_mesafesi_hesapla(hiz_ms, tepki_suresi=0.5):
    """Hıza (m/s) göre güvenli duruş mesafesini hesaplayıp döndürür."""
    tepkime_yolu = hiz_ms * tepki_suresi
    fren_yolu = (hiz_ms ** 2) / (2 * 7.5)  # 7.5 m/s^2 yavaşlama ivmesi
    toplam_mesafe = round(tepkime_yolu + fren_yolu, 2)
    return toplam_mesafe

# Döndürülen değeri bir değişkene atayıp başka bir koşulda kullanabiliriz
gereken_mesafe = fren_mesafesi_hesapla(15.0)
print(f"15 m/s hız için gereken duruş mesafesi: {gereken_mesafe} metre")
```

---

## 4. Fonksiyonların Modüler Kod Yazımına Katkısı
1. **Kod Tekrarını Önler (DRY - Don't Repeat Yourself):** Aynı hesaplamayı 10 farklı yerde tekrar yazmak yerine tek bir fonksiyon yazarız ve 10 kez çağırırız.
2. **Bakım ve Güncelleme Kolaylığı:** Bir formül değiştiğinde yüzlerce satır kodu taramak yerine yalnızca ilgili fonksiyonun içini güncellemek yeterlidir.
3. **Okunabilirlik ve Hata Ayıklama (Debugging):** Büyük bir problemi küçük, bağımsız fonksiyonlara (`veri_dogrula()`, `gorev_ekle()`, `rapor_goster()`) bölmek hataların hangi adımda çıktığını anında bulmayı sağlar.
4. **Ekip Çalışmasına Uygunluk:** Takımdaki her geliştirici farklı bir fonksiyonu yazıp test ederek kolayca birleştirebilir.
