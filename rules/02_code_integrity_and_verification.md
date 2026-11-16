# 🛡️ CODE INTEGRITY, SECURITY & VERIFICATION PROTOCOL

> **ZORUNLU KURAL:** Hiçbir AI agent, yazdığı kodun derlendiğini ve çalıştığını ampirik olarak (build/test komutları ve runtime logları ile) doğrulamadan görevi "tamamlandı" ilan edemez.

---

## 🏛️ 1. KOD KALİTESİ VE STRICT TYPE SAFETY

1. **Strict TypeScript Typing:**
   - Kod içerisinde `any` tipi veya `as unknown as Type`, `// @ts-ignore`, `// @ts-expect-error`, `/* eslint-disable */` ile tip kontrolünü atlatmak kesinlikle YASAKTIR. Tüm API yanıtları, props ve state'ler strict arayüzler (`interface` / `type`) ile tiplenecektir.
2. **Null & Undefined Guards:**
   - `.toFixed()`, `.map()`, `.length`, `.slice()` gibi metod çağrılarında null crash riskine karşı `(val ?? 0).toFixed(2)` şeklinde guard konulacaktır.
3. **XSS Güvenlik Protokolü:**
   - HTML içeriği render ederken `dangerouslySetInnerHTML` kullanmak sakıncalıdır. Zorunlu olmayan durumlarda düz metin `{text}` veya sanitize edilmiş parser kullanılmalıdır.
4. **Environment Variables:**
   - Client-side ortama sızmaması gereken gizli API anahtarları `NEXT_PUBLIC_` öneki alamaz.
   - Gizli anahtarlarda fallback olarak boş string (`|| ""`) veya sahte değer vermek KESİNLİKLE YASAKTIR. Eksik ortam değişkenleri Zod ile başlangıçta (`env.ts`) doğrulanmalıdır. Statik derleme/CI ortamında eksik anahtarların build kırmaması için `skipValidation: !!process.env.SKIP_ENV_VALIDATION` deseni desteklenmeli; çalışma zamanında ise fail-fast olunmalıdır.

---

## 🧪 2. İKİ AŞAMALI GERÇEK DOĞRULAMA KAPISI (STATIC + REAL RUNTIME)

> ⚠️ **`tsc` / `npm run build` tek başına GERÇEK TEST DEĞİLDİR.** Derlemenin geçmesi yalnızca sözdizimi ve tiplerin tutarlı olduğunu kanıtlar; uygulamanın çalıştığını kanıtlamaz.

1. **Aşama 1 — Statik Derleme Kapısı (Gerekli ama Yetersiz):**
   - `npm run build` / `npx tsc --noEmit` (veya ilgili dilin derleyicisi) Exit Code 0 vermelidir.
2. **Aşama 2 — Gerçek Çalışma Zamanı & E2E Testi (Zorunlu):**
   - **UI / Full-Stack:** Canlı sunucu (`localhost`) ayağa kaldırılıp **gerçek tarayıcıda** (Playwright E2E veya `browser` subagent / `browsermcp`) test edilmelidir: tıklama, form gönderme, sayfa yenileme sonrası kalıcılık, `console.error` / `pageerror` sıfırlığı, ağda beklenmedik `4xx/5xx` olmaması ve mobil (`375px`) yatay taşma kontrolü.
   - **Backend / API / DB:** Mocklanmış birim testleri yerine gerçek çalışan endpoint'e HTTP istekleri veya gerçek test veritabanı üzerinden entegrasyon testleri (`200/201` başarı + `400/401/403/422` hata senaryoları + DB kalıcılığı) çalıştırılmalıdır.
   - **CLI / Kütüphane / Script:** Araç gerçek argümanlar ve örnek girdi dosyalarıyla uçtan uca çalıştırılıp gerçek stdout/stderr çıktısı, üretilen dosya ve exit code doğrulanmalıdır (statik `tsc` ile yetinilemez).
   - **Dürüst Kapsam Kuralı:** Eğer ortam kısıtı nedeniyle canlı sunucu veya tarayıcı testi çalıştırılamadıysa, ajan *"Sadece statik build/typecheck geçti; canlı çalışma zamanı ve E2E DOĞRULANMADI"* demek zorundadır.
   - **Sahte Doğrulama Yasağı (Anti-Self-Attestation):** `Autonomous Task Audit Summary` karnesinde bildirilen her doğrulama (hem statik hem canlı test), oturumda fiilen çalıştırılmış komutun veya tarayıcı/API testinin gözlemlenen gerçek çıktı kanıtını içermek ZORUNDADIR.
   - **Kümülatif 3 Deneme Sınırı (Circuit Breaker):** Eğer düzeltmeler toplamda 3 denemede (`attempts <= 3`) hatayı sıfırlayamazsa, ajan sonsuz döngüye girmeden durmalı ve kök nedeni terminal çıktılarıyla kullanıcıya raporlamalıdır. Hata türü veya dosya değiştiğinde sayaç **kesinlikle sıfırlanmaz**.
   - **Genişletilmiş Yıkıcı Komut Yasağı:** Otonom düzeltme esnasında `git reset --hard`, `git clean -fd`, `git checkout -- .`, `git restore .`, `rm -rf`, `DROP TABLE`, `npm install --force` komutları ve mevcut dosyayı `read_file` ile okumadan `write_file` (`Overwrite: true`) ile körlemesine ezmek kesinlikle YASAKTIR.
2. **4 Bütünlük Sütunu Denetimi:**
   - **1. CSS/Stil Bütünlüğü** (Taşma, kırılma yok)
   - **2. DOM/İçerik Bütünlüğü** (Boş beyaz ekran riski yok)
   - **3. Varlıklar Bütünlüğü** (Kırık imaj/font yok)
   - **4. JS Etkileşim Bütünlüğü** (Butonlar ve yönlendirmeler tıklandığında çalışıyor)
