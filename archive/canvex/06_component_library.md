# 🧱 BİLEŞEN KÜTÜPHANESİ (Component Library Standards)
> **Sürüm:** 1.0 | CANVEX BugHunter & Finans Terminali  
> **Kural:** Bu dosyadaki standartlar harfi harfine uygulanır. Bileşen başına tek bir stil kararı verilir ve tutarlılık asla bozulmaz.

---

## 1. KART (Card)

```css
/* Temel Kart */
.card {
  background: var(--bg-card);
  border: 1px solid var(--border-subtle);
  border-radius: var(--radius-xl);     /* 16px */
  padding: 1.5rem;
  box-shadow: var(--shadow-card);
  transition: border-color var(--transition-base), box-shadow var(--transition-base);
}

/* Hover — SADECE border güçlenir, glow/renk değil */
.card:hover {
  border-color: var(--border-medium);
  box-shadow: var(--shadow-md);
}

/* Vurgulu Kart (metrik, özet) */
.card--highlighted {
  background: linear-gradient(135deg, var(--bg-card), rgba(37,99,235,0.04));
  border-color: var(--brand-border);
}

/* ❌ YASAK: .card:hover { border-color: #ef4444; box-shadow: 0 0 20px red; } */
```

**Kural:** Kartlarda hover'da kırmızı veya renkli glow YASAKTIR. Sadece border tonu güçlenir.

---

## 2. BUTON HİYERARŞİSİ (Button Hierarchy)

```css
/* === PRIMARY (Ana CTA) === */
.btn-primary {
  background: var(--brand-600);
  color: #ffffff;
  border: none;
  border-radius: var(--radius-md);    /* 10px */
  padding: 0.625rem 1.25rem;
  font-family: var(--font-body);
  font-size: 0.875rem;
  font-weight: 600;
  cursor: pointer;
  display: inline-flex;
  align-items: center;
  gap: 0.5rem;
  transition: background var(--transition-base), transform var(--transition-fast);
}
.btn-primary:hover {
  background: var(--brand-700);
  transform: translateY(-1px);
}
.btn-primary:active { transform: translateY(0); }

/* === SECONDARY (İkincil) === */
.btn-secondary {
  background: transparent;
  color: var(--text-secondary);
  border: 1px solid var(--border-subtle);
  border-radius: var(--radius-md);
  padding: 0.625rem 1.25rem;
  font-size: 0.875rem;
  font-weight: 600;
  cursor: pointer;
  transition: all var(--transition-base);
}
.btn-secondary:hover {
  border-color: var(--border-medium);
  color: var(--text-primary);
  background: rgba(255,255,255,0.04);
}

/* === GHOST (Hafif) === */
.btn-ghost {
  background: rgba(255,255,255,0.04);
  color: var(--text-secondary);
  border: 1px solid transparent;
  border-radius: var(--radius-md);
  padding: 0.5rem 1rem;
  font-size: 0.875rem;
  font-weight: 500;
  cursor: pointer;
  transition: all var(--transition-base);
}
.btn-ghost:hover {
  background: rgba(255,255,255,0.08);
  color: var(--text-primary);
}

/* === DANGER (Tehlikeli) === */
.btn-danger {
  background: var(--color-bear-bg);
  color: var(--color-bear);
  border: 1px solid var(--color-bear-border);
  border-radius: var(--radius-md);
  padding: 0.625rem 1.25rem;
  font-size: 0.875rem;
  font-weight: 600;
  cursor: pointer;
  transition: all var(--transition-base);
}
.btn-danger:hover {
  background: rgba(244,63,94,0.18);
}
```

---

## 3. BADGE / ROZET (Badge System)

```css
/* === TEMEL BADGE — Tüm rozetler rounded-full === */
.badge {
  display: inline-flex;
  align-items: center;
  gap: 0.3rem;
  padding: 0.2rem 0.65rem;
  border-radius: var(--radius-full);   /* 9999px — TAM YUVARLAK */
  font-size: 0.72rem;
  font-weight: 700;
  text-transform: uppercase;
  letter-spacing: 0.05em;
  white-space: nowrap;
}

/* Durum rozetleri */
.badge--critical {
  background: var(--color-bear-bg);
  color: var(--color-bear);
  border: 1px solid var(--color-bear-border);
}
.badge--warn {
  background: var(--color-warn-bg);
  color: var(--color-warn);
  border: 1px solid var(--color-warn-border);
}
.badge--ok, .badge--resolved {
  background: var(--color-bull-bg);
  color: var(--color-bull);
  border: 1px solid var(--color-bull-border);
}
.badge--info {
  background: var(--color-info-bg);
  color: var(--color-info);
  border: 1px solid var(--color-info-border);
}
.badge--neutral {
  background: rgba(255,255,255,0.06);
  color: var(--text-secondary);
  border: 1px solid var(--border-subtle);
}

/* Öncelik rozetleri — dolu arka plan */
.badge--p0 { background: var(--color-bear); color: #fff; border: none; }
.badge--p1 { background: var(--color-warn); color: #fff; border: none; }
.badge--p2 { background: var(--color-info); color: #fff; border: none; }
```

---

## 4. VERİ TABLOSU (Data Table)

```css
/* === TABLO KAPSAYICI === */
.table-wrapper {
  background: var(--bg-card);
  border: 1px solid var(--border-subtle);
  border-radius: var(--radius-xl);
  overflow: hidden;
}

.data-table {
  width: 100%;
  border-collapse: collapse;
}

/* Başlık satırı */
.data-table th {
  background: rgba(255,255,255,0.025);
  color: var(--text-secondary);
  font-family: var(--font-body);
  font-size: 0.7rem;
  font-weight: 700;
  text-transform: uppercase;
  letter-spacing: 0.07em;
  padding: 0.75rem 1rem;
  border-bottom: 1px solid var(--border-subtle);
  text-align: left;
  white-space: nowrap;
}

/* Veri hücreleri — ZORUNLU: font-mono */
.data-table td {
  font-family: var(--font-mono);
  font-size: 0.84rem;
  color: var(--text-primary);
  padding: 0.875rem 1rem;
  border-bottom: 1px solid var(--border-base);
  vertical-align: middle;
}

/* Sayısal sütunlar sağa yasla */
.data-table td.col-numeric,
.data-table th.col-numeric {
  text-align: right;
  font-variant-numeric: tabular-nums;
}

/* Satır hover */
.data-table tr:hover td {
  background: rgba(255,255,255,0.02);
}

/* Son satırda alt border yok */
.data-table tr:last-child td { border-bottom: none; }
```

---

## 5. INPUT / FORM ELEMANLARI

```css
/* === METİN GİRİŞİ === */
.form-input {
  background: var(--bg-surface);
  border: 1px solid var(--border-subtle);
  border-radius: var(--radius-md);    /* 10px */
  color: var(--text-primary);
  font-family: var(--font-body);
  font-size: 0.875rem;
  padding: 0.625rem 0.875rem;
  width: 100%;
  outline: none;
  transition: border-color var(--transition-base), box-shadow var(--transition-base);
}
.form-input::placeholder { color: var(--text-tertiary); }
.form-input:focus {
  border-color: var(--brand-500);
  box-shadow: 0 0 0 3px var(--brand-glow);
}

/* === SELECT === */
.form-select {
  appearance: none;
  background: var(--bg-surface);
  border: 1px solid var(--border-subtle);
  border-radius: var(--radius-md);
  color: var(--text-secondary);
  font-size: 0.875rem;
  padding: 0.625rem 2rem 0.625rem 0.875rem;
  cursor: pointer;
  outline: none;
  transition: border-color var(--transition-base);
}
.form-select:focus { border-color: var(--brand-500); }
```

---

## 6. METRİK KUTU (Metric Box)

```css
/* === FİNANSAL METRİK KARTI === */
.metric-card {
  background: var(--bg-card);
  border: 1px solid var(--border-subtle);
  border-radius: var(--radius-xl);
  padding: 1.25rem 1.5rem;
  display: flex;
  flex-direction: column;
  gap: 0.4rem;
}

/* Etiket */
.metric-label {
  font-size: 0.7rem;
  font-weight: 700;
  text-transform: uppercase;
  letter-spacing: 0.08em;
  color: var(--text-secondary);
}

/* Ana değer — ZORUNLU: font-mono + tabular-nums */
.metric-value {
  font-family: var(--font-mono);
  font-size: 1.875rem;
  font-weight: 700;
  color: var(--text-primary);
  font-variant-numeric: tabular-nums;
  letter-spacing: -0.02em;
  line-height: 1;
}

/* Değişim göstergesi */
.metric-delta {
  font-family: var(--font-mono);
  font-size: 0.8rem;
  font-weight: 600;
  font-variant-numeric: tabular-nums;
}
.metric-delta.positive { color: var(--color-bull); }
.metric-delta.negative { color: var(--color-bear); }
```

---

## 7. KOD / LOG KUTUSU

```css
/* === TERMİNAL / LOG KUTUSU === */
.log-box {
  background: var(--bg-base);
  border: 1px solid var(--border-subtle);
  border-left: 3px solid var(--brand-500);  /* Sol vurgu çizgisi */
  border-radius: var(--radius-md);
  padding: 0.875rem 1rem;
  font-family: var(--font-mono);
  font-size: 0.8rem;
  color: #4ade80;
  white-space: pre-wrap;
  overflow-x: auto;
  line-height: 1.6;
}

/* Satır numaraları */
.log-box .log-line-num {
  user-select: none;
  color: var(--text-tertiary);
  margin-right: 1rem;
  display: inline-block;
  min-width: 2rem;
  text-align: right;
}
```

---

## 8. İLERLEME ÇUBUĞU (Progress Bar)

```css
/* === ROADMAP PROGRESS BAR === */
.progress-track {
  height: 6px;
  background: rgba(255,255,255,0.06);
  border-radius: var(--radius-full);
  overflow: hidden;
}

.progress-fill {
  height: 100%;
  border-radius: var(--radius-full);
  transition: width 0.5s ease;
  /* Renk semantiğe göre */
}
.progress-fill.state-ok       { background: var(--color-bull); }
.progress-fill.state-warn     { background: var(--color-warn); }
.progress-fill.state-critical { background: var(--color-bear); }
.progress-fill.state-neutral  { background: var(--brand-500); }
/* ❌ YASAK: background: #ef4444 — her zaman semantic class kullan */
```

---

## 📐 BORDER-RADIUS STANDART TABLOSU

| Bileşen | CSS Değeri | Token |
|---|---|---|
| Büyük modal, hero kart | `20px` | `--radius-2xl` |
| Normal kart, panel, section | `16px` | `--radius-xl` |
| Küçük kart, dropdown item | `14px` | `--radius-lg` |
| Buton, input, tab, select | `10px` | `--radius-md` |
| Tooltip, kod etiketi | `6px` | `--radius-sm` |
| Badge, chip, avatar, dot | `9999px` | `--radius-full` |
| **0px / sıfır köşe** | **KESİNLİKLE YASAK** | — |
