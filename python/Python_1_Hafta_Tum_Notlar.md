# 1. Hafta: Python Giriş — Kapsamlı Ders ve Anlatım Notları

**Hazırlayan:** Ali İhsan Dağaşan  
**Takım:** Uludağ Üniversitesi Yapay Zeka Topluluğu — TALOS Otonom Araç Takımı  

> *Bu doküman, 1. Hafta Python Giriş föyündeki tüm konu başlıklarını (2.1 – 2.7) ve sunum/mülakat sırasında sorulabilecek temel soru-cevapları tek bir dosyada birleştirmektedir.*

---

## 2.1 Değişkenler ve Veri Tipleri
- **Temel Veri Tipleri:**
  - `int` (Tam sayı): `hiz = 50`, `kat_sayisi = -2`
  - `float` (Ondalıklı sayı): `mesafe = 12.75`, `pi = 3.14`
  - `str` (Metin / Karakter dizisi): `takim = "TALOS"`
  - `bool` (Mantıksal): `aktif = True` veya `False`
- **`type()` Kullanımı:** Değişkenin bellekteki veri tipini döndürür (`type(12.5)` → `<class 'float'>`).
- **`input()` Kullanımı:** Kullanıcıdan klavyeyle veri alır. **Her zaman `str` döndürür**, bu nedenle sayısal işlemlerde `int(input(...))` veya `float(input(...))` ile tip dönüşümü yapılır.

---

## 2.2 Operatörler
- **Aritmetik Operatörler:** `+` (Toplama), `-` (Çıkarma), `*` (Çarpma), `/` (Ondalıklı Bölme), `%` (Mod / Kalan bulma), `//` (Tam Bölme), `**` (Üs alma).
- **Karşılaştırma Operatörleri:** `==` (Eşittir), `!=` (Eşit değildir), `>` (Büyüktür), `<` (Küçüktür), `>=` (Büyük eşittir), `<=` (Küçük eşittir). Sonuç olarak `True` veya `False` üretir.
- **Mantıksal Operatörler:**
  - `and`: Tüm koşullar doğruysa `True` döner.
  - `or`: En az bir koşul doğruysa `True` döner.
  - `not`: Koşulun tersini alır (`not True` → `False`).

---

## 2.3 Koşul Yapıları (`if`, `elif`, `else`)
- Programın akışını belirli şartlara göre yönlendirir.
- **İç İçe Koşullar (Nested Conditions):** Bir ana koşul sağlandıktan sonra alt doğrulama gerektiğinde kullanılır *(Örn: Önce kullanıcı girişi doğru mu bakılır, doğruysa içerdeki `if` ile kullanıcının yetki rolü `admin` mi yoksa `operatör` mü kontrol edilir)*.

---

## 2.4 Fonksiyonlar (`def`)
- `def fonksiyon_adi(parametre1, parametre2):` şeklinde tanımlanır.
- **`return` İfadesi:** Fonksiyon içinde hesaplanan sonucu fonksiyonun çağrıldığı satıra geri döndürür.
- **Modüler Kod Yazımına Katkısı:** Kod tekrarını engeller (DRY prensibi), kodu okunabilir ve test edilebilir küçük parçalara böler, hata ayıklamayı ve bakımı kolaylaştırır.

---

## 2.5 Döngüler (`for`, `while`, `break`, `continue`)
- **`for` Döngüsü:** Liste, tuple, sözlük veya `range()` üzerinde eleman eleman gezinmek için kullanılır.
- **`while` Döngüsü:** Belirli bir koşul `True` kaldığı sürece çalışmaya devam eder (menü döngüleri, sensör okuma döngüleri).
- **`break`:** Döngüyü tamamen sonlandırır.
- **`continue`:** O anki turu atlayıp döngünün sıradaki turuna geçer.

---

## 2.6 Liste (`list`), Tuple (`tuple`), Dict (`dict`), Set (`set`)
- **`list` `[1, 2, 3]`:** Sıralı, değiştirilebilir (`append`, `remove`, `pop`, `sort`), tekrarlı elemana izin verir.
- **`tuple` `(1, 2, 3)`:** Sıralı fakat **değiştirilemez (immutable)** (`count`, `index`). Sabit koordinatlar ve ayarlar için idealdir.
- **`dict` `{"ad": "TALOS", "hiz": 40}`:** Anahtar-Değer (`Key-Value`) yapısındadır (`get`, `keys`, `values`, `items`, `pop`).
- **`set` `{"Kamera", "LiDAR"}`:** Sırasızdır ve **tekrarlı eleman barındırmaz** (`add`, `union`, `intersection`).

---

## 2.7 Sınıflar (`class`) ve Nesne Tabanlı Programlama (OOP)
- **`class`:** Nesnelerin özelliklerini (attribute) ve davranışlarını (method) tanımlayan şablondur.
- **`__init__(self, ...)`:** Sınıftan yeni bir nesne üretildiğinde otomatik çalışan kurucu (constructor) metottur.
- **`self`:** O an oluşturulan veya işlem yapılan nesnenin kendisini temsil eder; nesneye ait değişkenlere `self.degisken` şeklinde erişilir.

---

## 2.8 Antigravity Uygulaması, Antigravity IDE ve `.agents` Klasörü
- **Antigravity IDE & Uygulaması:** Google'ın AI-First (yapay zeka ajan odaklı) geliştirme ortamıdır. IDE tarafı VS Code tabanlı olup `Tab` tamamlama, `Ctrl+I` satır içi düzenleme ve `Agent Mode` (çok adımlı kodlama/terminal yönetimi) sunarken; Masaüstü Uygulaması (Antigravity 2.0) projeleri, arka plan görevlerini ve alt ajanları (subagents) yönetir.
- **`.agents` Klasörü Ne İşe Yarar?** Proje kök dizininde oluşturulan `.agents/` klasörü, yapay zeka ajanını o projeye özel olarak özelleştirmeye yarar. Antigravity bu klasörü otomatik olarak keşfeder (Auto-Discovery) ve en yüksek öncelikle (Workspace Priority) uygular. GitHub'a yüklendiğinde tüm takım üyelerinin ajanı aynı standartlarla çalışır.
- **`.agents` İçindeki Temel Yapılar:**
  - `rules/` (veya `AGENTS.md` / `GEMINI.md`): Ajanın kod yazarken uyması gereken proje kuralları ve kısıtlamalar (ör. PEP 8 uyumu, satır sınırı, isimlendirme kuralları).
  - `skills/<yetenek_adi>/SKILL.md`: Ajana çok adımlı özel bir iş akışını öğreten, sadece ihtiyaç duyulduğunda bağlama yüklenen (Progressive Disclosure) kılavuzlar.
  - `plugins/`, `hooks.json`, `mcp_config.json`: Eklenti paketleri, yaşam döngüsü tetikleyicileri ve dış servis (MCP) bağlantıları.

---

## Anlatım ve Soru-Cevap İçin Hızlı Hazırlık Rehberi

1. **`input()` ile aldığımız sayıyı neden direkt toplayamayız?**  
   Çünkü `input()` her zaman `str` (metin) döndürür. `"5" + "3"` işlemi toplama değil metin birleştirme yapar ve `"53"` verir. Matematiksel işlem için `int()` veya `float()` kullanılmalıdır.
2. **`print` ile `return` arasındaki fark nedir?**  
   `print` sadece ekrana çıktı verir, fonksiyon dışına değer taşımaz (`None` döner). `return` ise üretilen değeri çağrıldığı yere veri olarak döndürür, böylece başka işlemlerde kullanabiliriz.
3. **`list` ile `tuple` arasındaki en önemli fark nedir?**  
   Listeler değiştirilebilir (`mutable`), Tuple'lar değiştirilemez (`immutable`).
4. **Sınıflarda `__init__` ve `self` ne işe yarar?**  
   `__init__` nesne oluşturulurken başlangıç özelliklerini atayan yapıcı metottur; `self` ise üretilen her nesnenin kendi verilerini birbirine karıştırmadan tutmasını sağlayan nesne referansıdır.
