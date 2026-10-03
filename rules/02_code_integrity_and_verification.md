# 🛡️ CODE INTEGRITY, SECURITY & VERIFICATION PROTOCOL

> **ZORUNLU KURAL:** Hiçbir AI agent, yazdığı kodun derlendiğini ve çalıştığını ampirik olarak (build/test komutları ve runtime logları ile) doğrulamadan görevi "tamamlandı" ilan edemez.

---

## 🏛️ 1. KOD KALİTESİ VE STRICT TYPE SAFETY

1. **Strict TypeScript Typing:**
   - Kod içerisinde `any` tipi kullanımı kesinlikle YASAKTIR. Tüm API yanıtları, props ve state'ler strict arayüzler (`interface` / `type`) ile tiplenecektir.
2. **Null & Undefined Guards:**
   - `.toFixed()`, `.map()`, `.length`, `.slice()` gibi metod çağrılarında null crash riskine karşı `(val ?? 0).toFixed(2)` şeklinde guard konulacaktır.
3. **XSS Güvenlik Protokolü:**
   - HTML içeriği render ederken `dangerouslySetInnerHTML` kullanmak sakıncalıdır. Zorunlu olmayan durumlarda düz metin `{text}` veya sanitize edilmiş parser kullanılmalıdır.
4. **Environment Variables:**
   - Client-side ortama sızmaması gereken gizli API anahtarları `NEXT_PUBLIC_` öneki alamaz.
   - Gizli anahtarlarda fallback olarak boş string (`|| ""`) veya sahte değer vermek KESİNLİKLE YASAKTIR. Eksik ortam değişkenleri Zod ile başlangıçta (`env.ts`) doğrulanmalı ve deploy/başlatma anında fail-fast olunmalıdır.

---

## 🧪 2. AMPİRİK DOĞRULAMA VE VERIFICATION LOOP

1. **Dinamik Derleme ve Tip Kontrolü:**
   - TypeScript / Next.js projelerinde `npm run build` veya `npx tsc --noEmit`, Python projelerinde test/syntax kontrolü, diğer ekosistemlerde projenin derleme komutu çalıştırılmalı ve Exit Code 0 alındığı doğrulanmalıdır.
2. **4 Bütünlük Sütunu Denetimi:**
   - **1. CSS/Stil Bütünlüğü** (Taşma, kırılma yok)
   - **2. DOM/İçerik Bütünlüğü** (Boş beyaz ekran riski yok)
   - **3. Varlıklar Bütünlüğü** (Kırık imaj/font yok)
   - **4. JS Etkileşim Bütünlüğü** (Butonlar ve yönlendirmeler tıklandığında çalışıyor)
