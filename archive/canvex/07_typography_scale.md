# 🔤 TİPOGRAFİ & ÖLÇEK SİSTEMİ (Typography Scale)
> **Sürüm:** 1.0 | CANVEX BugHunter & Finans Terminali  
> **Kural:** Finans uygulamalarında tipografi = veri okunabilirliği. Her sayısal veri monospace ve tabular-nums olmalıdır.

---

## 🎯 FONT STACK VE YÜKLENDİĞİ ADRES

```html
<!-- Google Fonts CDN — head içinde zorunlu -->
<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
<link href="https://fonts.googleapis.com/css2?
  family=Sora:wght@600;700;800&
  family=Inter:wght@400;500;600;700&
  family=JetBrains+Mono:wght@400;500;600;700&
  display=swap" rel="stylesheet">
```

| Değişken | Font Ailesi | Kullanım Alanı |
|---|---|---|
| `--font-display` | Sora → Plus Jakarta Sans → system-ui | Sayfa başlıkları (h1, h2), marka metni, hero |
| `--font-body` | Inter → Plus Jakarta Sans → system-ui | Gövde, paragraf, etiket, buton, tablo başlığı |
| `--font-mono` | JetBrains Mono → Fira Code → monospace | TÜM sayısal veriler, kod blokları, terminal çıktısı |

---

## 📏 BAŞLIK HİYERARŞİSİ

```css
/* H1 — Sayfa başlığı, tek başına kullanılır */
h1 {
  font-family: var(--font-display);
  font-size: 1.875rem;     /* 30px */
  font-weight: 800;
  letter-spacing: -0.03em;
  color: var(--text-primary);
  line-height: 1.2;
}

/* H2 — Bölüm başlığı */
h2 {
  font-family: var(--font-display);
  font-size: 1.375rem;     /* 22px */
  font-weight: 700;
  letter-spacing: -0.02em;
  color: var(--text-primary);
  line-height: 1.3;
}

/* H3 — Kart/panel başlığı */
h3 {
  font-family: var(--font-display);
  font-size: 1.125rem;     /* 18px */
  font-weight: 600;
  letter-spacing: -0.01em;
  color: var(--text-primary);
  line-height: 1.4;
}

/* H4 — Alt başlık, tablo grup başlığı */
h4 {
  font-family: var(--font-body);
  font-size: 0.9375rem;    /* 15px */
  font-weight: 600;
  color: var(--text-primary);
  line-height: 1.5;
}
```

---

## 📊 FİNANSAL VERİ TİPOGRAFİSİ (ZORUNLU KURALLAR)

### Kural 1: Tüm Sayılar `font-mono` + `tabular-nums`

```css
/* ZORUNLU — finansal veri sınıfı */
.financial-data,
.data-table td,
.metric-value,
.price-display,
.percentage,
.volume-data {
  font-family: var(--font-mono) !important;
  font-variant-numeric: tabular-nums;
  letter-spacing: -0.01em;
}
```

### Kural 2: Sayısal Sütunlar Sağa Yaslanır

```css
/* Tablo sayısal sütun — sağa yasla */
.data-table td.col-numeric,
.data-table th.col-numeric {
  text-align: right;
  padding-right: 1.25rem;
}
```

### Kural 3: Renk Semantiği Tutarlı

```css
.value-positive { color: var(--color-bull); }  /* +%1.23 */
.value-negative { color: var(--color-bear); }  /* -%0.87 */
.value-neutral  { color: var(--text-primary); } /* değişim yok */
```

---

## 🏷️ ETIKET / LABEL SİSTEMİ

```css
/* Üst bağlam etiketi — tüm uppercase etiketler */
.label-uppercase {
  font-family: var(--font-body);
  font-size: 0.7rem;
  font-weight: 700;
  text-transform: uppercase;
  letter-spacing: 0.08em;
  color: var(--text-secondary);
  line-height: 1;
}

/* Normal etiket */
.label {
  font-size: 0.8125rem;  /* 13px */
  font-weight: 500;
  color: var(--text-secondary);
}

/* Küçük yardımcı metin */
.text-helper {
  font-size: 0.75rem;   /* 12px */
  color: var(--text-tertiary);
  line-height: 1.5;
}
```

---

## ⚡ BÜYÜK METRİK ÖLÇEĞI

| Boyut | Font-size | Font | Kullanım |
|---|---|---|---|
| `hero` | `3rem` / 48px | mono, 800 | Tek kritik metrik (ana dashboard) |
| `xl` | `1.875rem` / 30px | mono, 700 | Metric card ana değer |
| `lg` | `1.5rem` / 24px | mono, 600 | İkincil metrik |
| `md` | `1.125rem` / 18px | mono, 600 | Tablo özet satırı |
| `sm` | `0.875rem` / 14px | mono, 500 | Normal tablo verisi |
| `xs` | `0.75rem` / 12px | mono, 400 | Yardımcı veri, dipnot |

---

## 🚫 TİPOGRAFİ YASAKLARI

```
❌ YASAK:
  - Finansal sayılarda sans-serif font (font-mono zorunlu)
  - Sola yaslanmış fiyat/hacim verileri (text-right zorunlu)
  - font-variant-numeric olmadan büyük metrik değerler
  - 600px üzeri satır uzunluğu (max-width: 65ch kuralı)
  - 12px altında herhangi bir etiket veya gövde metni
  - Tamamen büyük harf (ALL CAPS) başlık — sadece uppercase etiketlere izin var

✅ DOĞRU:
  font-family: var(--font-mono);
  font-variant-numeric: tabular-nums;
  text-align: right;
```

---

## 📱 RESPONSIVE TİPOGRAFİ

```css
/* Mobile (< 640px) */
@media (max-width: 640px) {
  h1 { font-size: 1.5rem; }
  h2 { font-size: 1.125rem; }
  .metric-value { font-size: 1.5rem; }
}

/* Tablet (640px - 1024px) */
@media (max-width: 1024px) {
  h1 { font-size: 1.625rem; }
  .metric-value { font-size: 1.625rem; }
}
```
