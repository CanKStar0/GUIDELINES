# 🌐 GLOBAL AGENT EXECUTION PROTOCOL (TÜM PROJELER İÇİN GEÇERLİ ANA ANAYASA)

> **Son Güncelleme:** 11 Ekim 2026

## 🎯 TEMEL ÇALIŞMA VE ZORUNLU İCRA İLKESİ

Antigravity, Cursor, Claude veya herhangi bir AI runtime'ında çalışan TÜM Agent'lar aşağıdaki hiyerarşik protokole **%100 uymakla yükümlüdür**:

---

## ⚡ 1. HIZ, VERİMLİLİK & SIFIR İSRAF KURALLARI (ANTI-THRASHING STANDARDS)

### 🚫 A. Terminal Disiplini (run_command İsrafını Önleme)
- `run_command` aracı temel olarak paket yönetimi (`npm i`, `pnpm add`, `pip install`), derleme/tip kontrolü (`npm run build`, `npx tsc --noEmit`), test çalıştırma (`npm test`, `pytest`) ve bilinçli tekil proje analiz komutları (`git status`, `git ls-files`, `git grep`) için kullanılmalıdır.
- **YASAKTIR:** Amaçsız terminal döngüleri, terminal üzerinden rastgele dosya içeriği dökme (`cat`, `type`, `Get-Content`) veya kontrolsüz çıktı döngüleri (thrashing) KESİNLİKLE YASAKTIR. Dosya okuma ve inceleme işlemleri için Antigravity'nin yerel `view_file` aracı (hedef satır aralıklarıyla) kullanılmalıdır.

### 🧠 B. Tek Okuma Kuralı (In-Session Read Cache - Sıfır Tekrar)
- Bir dosya (ister bir `SKILL.md`, ister `package.json`, ister kaynak kodu) bu oturumda daha önce bir kez okunduysa, **içeriği zaten konuşma bağlamındadır.**
- Aynı dosyayı aynı oturumda körlemesine tekrar tekrar okumak (`view_file` döngüsü) KESİNLİKLE YASAKTIR. Ajan bağlamındaki mevcut bilgiyi kullanır.
- **İstisna:** Bir dosya üzerinde kod düzenlemesi (`replace_file_content` / `write_to_file`) yapıldıktan sonra satır kayması veya derleme hatası oluşursa, taze durumu doğrulamak için ilgili blok hedefli olarak yeniden okunabilir.

### 🎯 C. Nokta Atışı Okuma (Targeted Reads)
- Büyük dosyalarda körlemesine 800 satır okuma yapılmaz. Bilinen fonksiyon, route veya bileşen satır aralığı (`StartLine / EndLine`) hedeflenerek doğrudan ilgili blok incelenir.

### ⚡ D. Küçük İşler İçin Hızlı Şerit (Fast-Track Sınırı & Kriterleri)
- **Fast-Track İstisnası:** Sadece **en fazla 15 satırlık** önemsiz görsel düzeltme (renk/padding/tipografi) veya çoklu dil sözlüklerindeki (`en.json`, `tr.json`) senkron metin/çeviri değişiklikleri içeren durumlarda geçerlidir.
- **KESİN YASAK:** API rotaları, veritabanı şemaları/sorguları, kimlik doğrulama/güvenlik, ödeme akışları ve durum makineleri (state machines) KESİNLİKLE fast-track kapsamına GİREMEZ. Bu tür işlerde ilgili skill (`SKILL.md`) okunmadan koda dokunulamaz.

---

## 🛑 2. STEP 0: PRE-FLIGHT TOOL ÇAĞRI KİLİDİ (BÜYÜK / YENİ GÖREVLER İÇİN)
- Yeni bir mimari, sıfırdan bileşen, veritabanı tablosu veya API geliştirilirken:
  - Eğer ilgili uzmanlık (`SKILL.md`) bu sohbette **henüz hiç okunmadıysa**, koda dokunmadan önce ilk araç çağrısı o skill için `view_file` olmalıdır.
  - *Not:* Eğer bu oturumda o skill zaten okunduysa, kural 1-B gereği tekrar okunmaz; doğrudan koda geçilir.

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
- Kod değişikliği tamamlandığında projenin derleme ve test araçları ile (TypeScript/Next.js projelerinde `npm run build` / `npx tsc --noEmit`, Python'da `pytest`, diğer dillerde ilgili derleme aracı) ampirik doğrulama (Exit Code 0) alınmadan iş bitti sayılamaz.
- **Circuit Breaker (`attempts <= 3`):** Üst üste 3 denemede derleme veya test hataları çözülemezse sonsuz tamir döngüsüne girmeden durulmalı, terminal çıktıları ve kök neden özeti kullanıcıya iletilmelidir.
- **Yıkıcı Komut Yasağı:** Otonom düzeltme esnasında `git reset --hard`, `git clean -fd`, `rm -rf`, `DROP TABLE` gibi geri dönüşsüz komutlar kesinlikle çalıştırılamaz.
- Görev sonunda `Autonomous Task Audit Summary` karnesini kullanıcıya sun.
