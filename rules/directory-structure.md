# 📁 Proje Klasör ve Dosya Düzen Standartları (Directory Structure & File Placement Rules)

> **Amaç:** Kod tabanında script, test, dokümantasyon ve araçların düzensiz dağılmasını önlemek, tüm scriptlerin `docs/` klasörü içerisinde düzenli yer almasını sağlamak.

---

## 🏛️ KESİN DOSYA VE KLASÖR YERLEŞİM KURALLARI

1. **Script ve Araç Dosyaları (`scripts/` veya `tools/`):**
   - Proje için üretilen otomasyon scriptleri, seed/migration yardımcıları ve CLI araçları standart olarak projenin `scripts/` veya `tools/` klasöründe yer alır. Dokümantasyon rehberleri ise `docs/` altında toplanır.
   - Kök dizine rastgele saçılmış geçici scriptler bırakılamaz.

2. **Test Dosyaları (`tests/`, `test/` veya `__tests__/`):**
   - Senaryo testleri, birim (unit) testleri, entegrasyon testleri ve doğrulama scriptleri `tests/` klasörüne (veya framework konvansiyonu olan `__tests__` / `*.test.ts`) kaydedilir.

3. **Geçici Çıktılar ve Taslak Kodlar:**
   - Antigravity oturumu için geçici test scriptleri conversation scratch dizininde (`<appDataDir>\brain\<conversation-id>/scratch/`) tutulur.
   - Proje içi geçici debug çıktıları projenin `.gitignore` dosyasında bulunan `scratch/` veya `tmp/` altında toplanmalı, repoya commit edilmemelidir.

---

## 🔍 PROJE BAŞLANGICI VE ANALİZ PROTOKOLÜ

Her yeni projede veya mevcut projede çalışmaya başlarken AI Agent şu adımları uygular:
1. Projenin mevcut klasör yapısını inceler (projenin kendi mimari konvansiyonuna saygı gösterir).
2. Scriptlerin `scripts/` veya `tools/` altında toplandığını doğrular.
3. Test altyapısının varlığını teyit eder.
