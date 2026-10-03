# 🎨 RENK TOKEN SİSTEMİ (Color Token System)
> **Sürüm:** 2.0 — Kurumsal Finans Terminali Standardı  
> **Temel Kural:** Bu dosya SSOT (Single Source of Truth)'tur. Projede renk hard-code edilemez; tüm renkler bu token'lardan gelmelidir.

---

## 🧠 RENK PSİKOLOJİSİ İLKESİ

Finans terminalleri için renk psikolojisi araştırması (Bloomberg, TradingView, Koyfin standardı):

| Renk Grubu | Psikolojik Etki | CANVEX'te Kullanım Alanı |
|---|---|---|
| **Derin Siyah / Midnight Navy** | Otorite, güven, profesyonellik | Zemin katmanlar |
| **Electric Blue (#2563eb)** | Güvenilirlik, kararlılık, aksiyon | MARKA aksanı — sadece buton/aktif/link |
| **Teal/Emerald (#22d3a3)** | Büyüme, başarı, sofistike | Pozitif / yükseliş verileri |
| **Rose (#f43f5e)** | Uyarı, aciliyet (panik değil) | Negatif / düşüş / kritik hata |
| **Amber (#fb923c)** | Dikkat, enerji | Uyarı / P1 seviyesi |
| **Sky Blue (#38bdf8)** | Bilgi, açıklık, soğuk akıl | P2 / bilgilendirme |
| **Ham Kırmızı (#ef4444)** | Panik, alarm — kullanıcıyı rahatsız eder | **SADECE debug parlama halkası (Kural #1)** |

---

## 🎯 TEMEL KURAL — Tek Aksent Rengi

> **60-30-10 Kuralı:** 60% koyu nötr zemin + 30% ikincil nötr yüzeyler + **10% aksent** (electric blue).
> Aksent rengi sadece: CTA butonlar, aktif tab, link, seçili eleman.
> Hiçbir kart border'ı, ikon rengi veya dekoratif eleman aksent rengi alamaz.

---

## 🏗️ CSS CUSTOM PROPERTY TANIMLARI (Canonical)

```css
:root {
  /* ============================================
     KATMAN 1 — ZEMİN (DARK MODE)
  ============================================ */
  --bg-base:       #07090f;   /* En derin — body background */
  --bg-surface:    #0d1117;   /* Ana sayfa zemini */
  --bg-card:       #111827;   /* Kart, panel, section */
  --bg-elevated:   #1a2234;   /* Dropdown, tooltip, popover */
  --bg-overlay:    rgba(7,9,15,0.85); /* Modal, drawer backdrop */

  /* ============================================
     KATMAN 1 — ZEMİN (LIGHT MODE - future)
  ============================================ */
  --bg-base-light:     #ffffff;
  --bg-surface-light:  #f8fafc;
  --bg-card-light:     #f1f5f9;
  --bg-elevated-light: #e2e8f0;

  /* ============================================
     SINIR / ÇERÇEVE KATMANLARI
  ============================================ */
  --border-base:    rgba(255,255,255,0.05);  /* Çok ince — satır ayraçları */
  --border-subtle:  rgba(255,255,255,0.08);  /* Normal kart border */
  --border-medium:  rgba(255,255,255,0.12);  /* Hover, vurgulu */
  --border-strong:  rgba(255,255,255,0.20);  /* Fokus, seçili */

  /* ============================================
     TİPOGRAFİ (Metin Renkleri)
  ============================================ */
  --text-primary:    #f0f4ff;  /* Başlıklar, kritik sayılar */
  --text-secondary:  #94a3b8;  /* Alt başlıklar, etiketler */
  --text-tertiary:   #4b5563;  /* Placeholder, devre dışı */
  --text-accent:     #60a5fa;  /* Link, interaktif metin */
  --text-inverse:    #07090f;  /* Açık zemin üzerindeki metin */

  /* ============================================
     MARKA AKSANTİ — Electric Blue
     KURAL: SADECE CTA, aktif tab, link, seçili
  ============================================ */
  --brand-50:        #eff6ff;
  --brand-100:       #dbeafe;
  --brand-400:       #60a5fa;
  --brand-500:       #3b82f6;
  --brand-600:       #2563eb;   /* Ana CTA butonu */
  --brand-700:       #1d4ed8;   /* Hover durumu */
  --brand-900:       #1e3a8a;
  --brand-glow:      rgba(37,99,235,0.15);
  --brand-border:    rgba(37,99,235,0.25);

  /* ============================================
     SEMANTİK RENKLER
     KURAL: Sadece veri durumu için kullan
  ============================================ */

  /* Pozitif / Yükseliş / Başarı */
  --color-bull:         #22d3a3;
  --color-bull-bg:      rgba(34,211,163,0.10);
  --color-bull-border:  rgba(34,211,163,0.25);

  /* Negatif / Düşüş / Hata */
  --color-bear:         #f43f5e;
  --color-bear-bg:      rgba(244,63,94,0.10);
  --color-bear-border:  rgba(244,63,94,0.25);

  /* Uyarı / P1 */
  --color-warn:         #fb923c;
  --color-warn-bg:      rgba(251,146,60,0.10);
  --color-warn-border:  rgba(251,146,60,0.25);

  /* Bilgi / P2 */
  --color-info:         #38bdf8;
  --color-info-bg:      rgba(56,189,248,0.10);
  --color-info-border:  rgba(56,189,248,0.25);

  /* Nötr / İstatistik */
  --color-neutral:        #a78bfa;
  --color-neutral-bg:     rgba(167,139,250,0.10);
  --color-neutral-border: rgba(167,139,250,0.25);

  /* ============================================
     DEBUG PARLAMA HALKASI — Anayasa Kural #1
     KURAL: SADECE hata tespiti görsel işaretleme için
  ============================================ */
  --debug-error-neon:   #ef4444;
  --debug-glow-ring:    0 0 0 8px #000000, 0 0 30px rgba(239,68,68,0.95);

  /* ============================================
     TİPOGRAFİ FONT STACK
  ============================================ */
  --font-display: 'Sora', 'Plus Jakarta Sans', system-ui, sans-serif;
  --font-body:    'Inter', 'Plus Jakarta Sans', system-ui, sans-serif;
  --font-mono:    'JetBrains Mono', 'Fira Code', 'Cascadia Code', monospace;

  /* ============================================
     BORDER RADIUS (Standart)
  ============================================ */
  --radius-sm:   6px;    /* Tooltip */
  --radius-md:   10px;   /* Buton, input, tab, select */
  --radius-lg:   14px;   /* Küçük kart */
  --radius-xl:   16px;   /* Normal kart, panel */
  --radius-2xl:  20px;   /* Modal, büyük kart */
  --radius-full: 9999px; /* Badge, chip, avatar */
  /* NOT: 0px köşe (sıfır) kesinlikle YASAKTIR */

  /* ============================================
     GÖLGE SİSTEMİ
  ============================================ */
  --shadow-sm:   0 1px 3px rgba(0,0,0,0.4);
  --shadow-md:   0 4px 16px rgba(0,0,0,0.5);
  --shadow-lg:   0 8px 32px rgba(0,0,0,0.6);
  --shadow-xl:   0 16px 48px rgba(0,0,0,0.7);
  --shadow-card: 0 2px 8px rgba(0,0,0,0.3), 0 0 0 1px rgba(255,255,255,0.05);

  /* ============================================
     ANİMASYON SÜRELERİ
  ============================================ */
  --transition-fast:   0.12s ease;
  --transition-base:   0.20s ease-in-out;
  --transition-slow:   0.35s ease;
  /* YASAK: 0.5s üstü dekoratif animasyon */
}
```

---

## 🚫 YASAK RENKLER VE KULLANIM HATALARI

```
❌ YASAKTIR:
  #000000 veya #111111 → Zemin için ham siyah — yerine --bg-base kullan
  #ef4444 (debug kırmızısı) → Kart border, ikon, buton, progress'te kullanma
  Kırmızı hover glow → .card:hover'da crimson/red box-shadow YASAK
  Çiğ düz renkler → #f97316 (ham turuncu) yerine --color-warn kullan
  
✅ DOĞRU KULLANIM:
  border: 1px solid var(--border-subtle);
  background: var(--color-bull-bg);
  color: var(--color-bull);
  border-color: var(--brand-border);
```

---

## 🌓 LIGHT MODE GEÇIŞ KURALI

Light mode için `[data-theme="light"]` selector kullanılacak:

```css
[data-theme="light"] {
  --bg-base:      var(--bg-base-light);
  --bg-surface:   var(--bg-surface-light);
  --bg-card:      var(--bg-card-light);
  --text-primary: #0f172a;
  --text-secondary: #475569;
  --border-subtle: rgba(0,0,0,0.08);
  --border-medium: rgba(0,0,0,0.12);
}
```
