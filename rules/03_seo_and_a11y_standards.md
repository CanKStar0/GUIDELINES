# 🔍 SEO & ACCESSIBILITY (A11Y) STANDARDS

> **ZORUNLU KURAL:** Üretilen tüm web sayfaları arama motoru optimizasyonu (SEO) ve erişilebilirlik (a11y) standartlarına %100 uyumlu olmalıdır.

---

## 📌 1. SEO BEST PRACTICES

1. **Title & Meta Description:**
   - Her sayfanın özgün, tanımlayıcı bir `title` ve `description` meta etiketi olmalıdır.
2. **Heading Hiyerarşisi (H1-H6):**
   - Her sayfada **yalnızca 1 adet `<h1>`** bulunmalıdır. Başlıklar mantıksal hiyerarşi (`h1 -> h2 -> h3`) izlemelidir.
3. **Semantik HTML5:**
   - Sayfa yapısında `div` çorbası yerine `header`, `nav`, `main`, `section`, `article`, `aside`, `footer` semantik elemanları kullanılmalıdır.
4. **Programmatic SEO & Open Graph:**
   - Dinamik sayfalarda (`/stocks/[ticker]`) Open Graph (`og:title`, `og:description`, `og:image`) ve JSON-LD structured data mantığı korunmalıdır.

---

## ♿ 2. ERİŞİLEBİLİRLİK (A11Y) STANDARTLARI

1. **Aria Labels:**
   - Metin içermeyen tüm ikon butonlarında (`<button aria-label="Arama yap">`) zorunlu `aria-label` bulunacaktır.
2. **Focus Indicators:**
   - Klavye ile gezinmede görünür focus ring (`focus-visible:ring-2 focus-visible:ring-blue-500`) olmalıdır. `outline-none` tek başına bırakılamaz.
3. **WCAG AA Renk Kontrastı:**
   - Metin ve arka plan renkleri arasında WCAG AA standardını karşılayan yüksek kontrast oranı (en az 4.5:1) bulunmalıdır.
