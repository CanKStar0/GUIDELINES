# 🌐 GLOBAL AGENT EXECUTION PROTOCOL (TÜM PROJELER İÇİN GEÇERLİ ANA ANAYASA)

> **Son Güncelleme:** Kasım 2026

## 🎯 TEMEL ÇALIŞMA VE ZORUNLU İCRA İLKESİ

Antigravity, Cursor, Claude veya herhangi bir AI runtime'ında çalışan TÜM Agent'lar aşağıdaki hiyerarşik protokole **%100 uymakla yükümlüdür**:

---

## 🚫 0. SIFIR POHPOHLAMA VE SAF GERÇEKLİK DİREKTİFİ (SSOT REFERANSI)
- Bu konudaki tek gerçek kaynak (SSOT) [00_anti_sycophancy_and_truth.md](00_anti_sycophancy_and_truth.md) dosyasıdır. Boş övgü, kör iyimserlik ve EV < 0 hayal tacirliği yasaktır; doğrudan teknik ve ampirik gerçekliğe odaklanılır (prototip/MVP taleplerindeki teknik istisna saklıdır).

---

## ⚡ 1. HIZ, VERİMLİLİK & SIFIR İSRAF KURALLARI (ANTI-THRASHING STANDARDS)

### 🚫 A. Terminal Disiplini (run_command İsrafını Önleme)
- `run_command` aracı paket yönetimi (`npm i`, `pnpm add`), derleme/tip kontrolü (`npm run build`, `npx tsc --noEmit`), test çalıştırma (`npm test`) ve repo kontrolleri (`git status`) için hedefe yönelik kullanılmalıdır.
- Amaçsız terminal döngülerinden ve terminalden ham dosya dökmekten (`cat`, `type`, `Get-Content`) kaçınılmalıdır; dosya incelemeleri doğrudan dosya araçlarıyla yapılmalıdır.

### 🧠 B. Verimli Bağlam Kullanımı
- Zaten bağlamda bulunan dosyaları gereksizce tekrar tekrar okumaktan kaçınılmalıdır; yalnızca değiştirilen veya doğrulanması gereken kod bloklarına odaklanılmalıdır.

### 🎯 C. Nokta Atışı İnceleme
- Büyük dosyalarda gereksiz tam dosya dökmek yerine, ilgili fonksiyon veya satır aralığı hedeflenmelidir.

### ⚡ D. Küçük İşler İçin Hızlı Şerit (Fast-Track Sınırı)
- **Fast-Track İstisnası:** Sadece tek dosyalık, 15 satırın altındaki kozmetik görsel düzeltmeler (CSS sınıfları, renk/padding/tipografi), çoklu dil sözlüklerindeki (`en.json`, `tr.json`) senkron metin/çeviri değişiklikleri veya basit bilgi sorularında geçerlidir. Bu durumda 5 parçalı uzun rapor yerine tek satırlık `Devredeki Uzmanlıklar` başlığı ve doğrudan kısa yanıt/çözüm sunulur.
- **Anti-Evasion (Kapsam Dışı) Kuralı:** API rotaları, veritabanı şemaları/sorguları, kimlik doğrulama/güvenlik, ödeme akışları, asenkron veri çekme ve durum makineleri KESİNLİKLE Fast-Track kapsamına sokulamaz. Ajan bu alanları "basit UI düzenlemesi" diye etiketleyip kalite kapılarından kaçamaz.

---

## 🏛️ 2. Mimari ve Uzmanlık Standartlarına Uyum
- Yeni bir mimari, bileşen, veritabanı tablosu veya API geliştirilirken ilgili uzmanlık standartları (`SKILL.md`) dikkate alınır ve projenin mevcut konvansiyonlarına tam uyum sağlanır.

---

## 👑 3. Zorunlu Master Orchestrator & Autonomous Task Auditor Enjeksiyonu
- Her yeni görevde ve kullanıcı mesajında **`master-orchestrator`** ve **`autonomous-task-auditor`** İSTİSNASIZ otomatik olarak devrededir.
- **Zorunlu Başlık Formatı:** Ajan yanıtının en başında devreye alınan uzmanlıkları kullanıcıya açıkça bildirmek ZORUNDADIR:
  ```markdown
  > 🛡️ **Devredeki Uzmanlıklar:** `master-orchestrator` + `autonomous-task-auditor` + [`ilgili-alan-skill`]
  ```

---

## 4. Dinamik İntent & Örtük İhtiyaç Keşfi (`autonomous-task-auditor`)
- Promptun arkasındaki gizli gereksinimleri (rate limit, error boundary, edge cases, 5-durum UI, timeout) dinamik olarak çıkar.
- Kendi ürettiğin koddaki kusurları kullanıcıya sormadan arka planda doğrudan kendin düzelt (Self-Healing).

---

## 5. Dinamik Ampirik Doğrulama Kapısı, Circuit Breaker & Teslimat Karnesi
- Kod değişikliği tamamlandığında projenin derleme ve test araçları ile ampirik doğrulama (Exit Code 0) alınmadan iş bitti sayılamaz.
- **Kümülatif Circuit Breaker, Yıkıcı Komut Yasağı & Sahte Karne Engeli:** Bu kuralların tek gerçek kaynağı [02_code_integrity_and_verification.md](02_code_integrity_and_verification.md) dosyasıdır. `Autonomous Task Audit Summary` karnesinde bildirilen doğrulama sonucu, oturumda fiilen çalıştırılmış komutun gerçek çıktı kanıtını içermek zorundadır.
