# 2.8 Antigravity Uygulaması, Antigravity IDE ve `.agents` Klasörü

## 1. Antigravity Uygulaması ve Antigravity IDE Nedir?
**Google Antigravity (AGY)**, yazılım geliştirme sürecinde yapay zeka ajanlarıyla (AI Agents) birlikte çalışmayı sağlayan **AI-First (Yapay Zeka Odaklı)** bir geliştirme platformudur. İki temel arayüzü (surface) bulunur ve ikisi de aynı ajan altyapısını paylaşır:

1. **Antigravity IDE:**
   - VS Code tabanlı, doğrudan kod editörünün içine entegre edilmiş geliştirme ortamıdır.
   - **3 Temel Kullanım Modu Vardır:**
     - *Antigravity Tab (Pasif / Otomatik Tamamlama):* Kodu yazarken bağlama göre sonraki satırı, import'ları veya imleç sıçramalarını (`Tab` tuşuyla) tahmin eder.
     - *Inline Command (`Ctrl + I`):* Seçili bir kod bloğunu yerinde düzenlemek, açıklamak, yorum satırı eklemek veya yeni fonksiyon üretmek için kullanılır.
     - *Sidebar Chat & Agent Mode (İşbirlikçi Mod):* Sağ/sol paneldeki sohbet alanı üzerinden çok adımlı görevleri planlayan, dosyaları okuyup yazabilen ve terminalde test çalıştırabilen otonom eş-programcı (pair programmer) modudur.
2. **Antigravity Uygulaması (Antigravity 2.0 Desktop App):**
   - IDE'den bağımsız çalışan masaüstü uygulamasıdır.
   - Birden fazla projeyi yönetmek, arka planda çalışan görevleri (Background Tasks), alt ajanları (Subagents), zamanlanmış görevleri (Scheduled Tasks) ve üretilen raporları (Artifacts) tek bir kontrol merkezinden yönetmek için kullanılır.

---

## 2. `.agents` Klasörü Nedir ve Ne İşe Yarar?

Bir projenin kök dizininde (root) oluşturulan **`.agents/`** (veya `.agent/`) klasörü, **Antigravity Özelleştirme Sisteminin (Customization System)** proje bazlı merkezidir.

Normalde yapay zeka asistanları genel amaçlıdır; bizim projemizin özel kurallarını, takımımızın kodlama standartlarını veya iş akışlarını bilmezler. Projemizin içine `.agents` klasörü açtığımızda, Antigravity çalışma dizininden yukarı doğru çıkarken bu klasörü **otomatik olarak keşfeder (Auto-Discovery)** ve içindeki ayarları o projeye uygular.

### `.agents` Klasörünün Sağladığı En Büyük Avantajlar
1. **Projeye Özel Hafıza ve Kural Seti:** Her seferinde sohbete *"Kodları Türkçe yorum satırıyla yaz, 100 satırı geçme, PEP 8'e uy"* demek yerine bu kuralları `.agents` içine bir kez yazarız; ajan her zaman bu kurallara uyar.
2. **Git / GitHub ile Takım İçi Paylaşım:** `.agents/` klasörü proje klasörünün içinde olduğu için GitHub'a (`git push`) yüklendiğinde, projeyi bilgisayarına çeken (`git clone`) tüm TALOS takım üyelerinin Antigravity ajanı aynı kurallarla ve aynı yeteneklerle çalışır.
3. **Progressive Disclosure (Aşamalı Yükleme ile Bağlam Tasarrufu):** `.agents/skills/` içindeki tüm uzun dokümanlar aynı anda yapay zekanın hafızasını (context window) doldurmaz. Ajan önce sadece yeteneklerin kısa açıklamalarını (`description`) görür, yalnızca o işle ilgili bir görev geldiğinde ilgili `SKILL.md` dosyasını okur.

---

## 3. `.agents` Klasörünün İç Yapısı ve Bileşenleri

Bir `.agents` klasörünün içinde ihtiyacımıza göre şu alt bileşenler yer alır:

```text
proje-klasoru/
├── .agents/
│   ├── rules/                      # 1. Kurallar (Rules)
│   │   └── python-kurallari.md     # Kodlama standartları ve kısıtlamalar
│   ├── skills/                     # 2. Yetenekler / İş Akışları (Skills)
│   │   └── kod-test-et/
│   │       ├── SKILL.md            # Zorunlu ana talimat dosyası (YAML başlıklı)
│   │       └── scripts/            # Yardımcı betikler
│   ├── plugins/                    # 3. Eklenti Paketleri (Plugins)
│   │   └── <eklenti_adi>/plugin.json
│   ├── hooks.json                  # 4. Yaşam Döngüsü Kancaları (Hooks)
│   └── mcp_config.json             # 5. Dış Araç Bağlantıları (MCP Servers)
├── AGENTS.md (veya GEMINI.md)      # Dizin bazlı her zaman aktif kurallar
└── gorev_yoneticisi.py
```

### Bileşenlerin Görevleri
1. **Rules (`rules/*.md` veya kök dizinde `AGENTS.md` / `GEMINI.md`):**
   - Ajanın kod yazarken uyması gereken kurallardır *(Örn: "Değişken isimleri Türkçe ve snake_case olsun", "Fonksiyonlarda mutlaka docstring bulunsun")*.
2. **Skills (`skills/<yetenek-adi>/SKILL.md`):**
   - Ajana çok adımlı özel bir işi nasıl yapacağını öğreten kılavuzlardır (runbook/cheatsheet). Başında `name` ve `description` içeren bir YAML bloğu bulunur.
3. **Plugins (`plugins/<ad>/plugin.json`):**
   - Birden fazla skill, rule, hook ve MCP ayarını tek bir paket halinde gruplayıp açıp kapatmayı sağlar.
4. **Hooks (`hooks.json`):**
   - Ajan bir aracı çalıştırmadan hemen önce veya sonra otomatik olarak bir güvenlik/formatlama betiği tetiklemek için kullanılır.
5. **MCP Servers (`mcp_config.json`):**
   - Model Context Protocol (MCP) üzerinden ajanı dış servislere (veritabanları, GitHub, Jira, sensör simülasyon araçları vb.) bağlar.

---

## 4. Yükleme Önceliği (Loading Priority)
Eğer hem bilgisayar genelinde (`~/.gemini/config/`) hem de proje içindeki `.agents/` klasöründe aynı isimli bir kural veya skill varsa, Antigravity **en yüksek önceliği her zaman proje içindeki `.agents/` (Workspace Project) klasörüne verir**. Böylece projenin kendi kuralları genel ayarları ezer.

---

## 5. Anlatım ve Soru-Cevap İçin Kısa Özet (Kendi Cümlelerimizle Nasıl Anlatırız?)

- **Soru: `.agents` klasörü kısaca nedir?**  
  **Cevap:** Projemizin kök dizinine açtığımız, Antigravity yapay zeka ajanına o projede nasıl davranması gerektiğini, kodlama kurallarımızı (`rules`) ve özel iş akışlarımızı (`skills`) öğreten yapılandırma klasörüdür.
- **Soru: Neden ayarları genel ayarlarda tutmak yerine proje içinde `.agents` klasörüne koyuyoruz?**  
  **Cevap:** Çünkü projeyi GitHub'a yüklediğimizde `.agents` klasörü de repoyla birlikte gider. Böylece takımdaki herkes projeyi indirdiğinde yapay zeka asistanı tüm ekip üyelerinde aynı standartlarla çalışır.
- **Soru: `.agents` içindeki `rules` ile `skills` arasındaki fark nedir?**  
  **Cevap:** `rules` (kurallar), ajanın kod yazarken her zaman uyması gereken kısıtlamalar ve stil kurallarıdır (örneğin PEP 8'e uymak, 100 satırı geçmemek). `skills` (yetenekler) ise ajanın sadece belirli bir görev istendiğinde açıp okuduğu adım adım iş yapma kılavuzlarıdır (`SKILL.md`).
