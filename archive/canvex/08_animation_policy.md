# 🎬 ANİMASYON POLİTİKASI (Animation Policy)
> **Sürüm:** 1.0 | CANVEX BugHunter & Finans Terminali  
> **Temel İlke:** Finans terminallerinde animasyon bilgi iletmek için var, dikkat çekmek için değil. "Sıfır Oyuncak" ilkesi.

---

## ✅ İZİN VERİLEN ANİMASYONLAR

### 1. State Transition (Durum Geçişi)
```css
/* Hover, focus, active durum geçişleri — SADECE bu */
transition: color var(--transition-base);
transition: background var(--transition-base);
transition: border-color var(--transition-base);
transition: box-shadow var(--transition-base);
transition: opacity var(--transition-fast);
transition: transform var(--transition-fast);

/* Kullanım: --transition-base = 0.20s ease-in-out */
/* Kullanım: --transition-fast = 0.12s ease */
```

### 2. Micro-lift (Kart Hover)
```css
/* Hover'da hafif yükseltme — max 2px */
.card:hover {
  transform: translateY(-2px);  /* MAX -2px, daha fazlası YASAK */
}
```

### 3. Progress Bar Doldurma
```css
/* İlerleme çubuğu genişleme animasyonu */
.progress-fill {
  transition: width 0.5s ease;  /* Tek izin verilen 0.5s animasyon */
}
```

### 4. Sayfa İçi Görünürlük
```css
/* Görünür/gizli geçiş (modal, dropdown, tooltip) */
.modal {
  transition: opacity var(--transition-base), visibility var(--transition-base);
}
```

### 5. Skeleton Loading
```css
/* İçerik yüklenirken iskelet animasyonu */
@keyframes skeleton-shimmer {
  0%   { background-position: -200% 0; }
  100% { background-position: 200% 0; }
}
.skeleton {
  background: linear-gradient(90deg,
    rgba(255,255,255,0.04) 25%,
    rgba(255,255,255,0.08) 50%,
    rgba(255,255,255,0.04) 75%
  );
  background-size: 200% 100%;
  animation: skeleton-shimmer 1.5s ease infinite;
}
```

### 6. Debug Parlama Halkası (Anayasa Kural #1)
```css
/* BU ANIMASYON SADECE BUG DETECTION AMAÇLIDIR */
/* Kullanıcı arayüzünde asla kullanılmaz */
.debug-error-ring {
  outline: 5px dashed var(--debug-error-neon);
  box-shadow: var(--debug-glow-ring);
  animation: debug-pulse 1.5s ease infinite;
}
@keyframes debug-pulse {
  0%, 100% { box-shadow: var(--debug-glow-ring); }
  50%       { box-shadow: 0 0 0 8px #000, 0 0 50px rgba(239,68,68,0.5); }
}
```

---

## ❌ YASAK ANİMASYONLAR

```
❌ KESINLIKLE YASAK:

1. Süre limiti aşımı:
   - 0.5s üzerinde dekoratif animasyonlar
   - infinite loop eden neon/glow/renk döngüleri
   - Sayfa girişinde uzun intro animasyonlar (fade-in > 400ms)

2. Dikkat dağıtıcı keyframe'ler:
   - Zıplama (bounce), sallama (shake), titreme (vibrate)
   - Dönen/spinning arka plan elementleri
   - Yanıp sönen (blink) butonlar veya metinler
   - Neon glow pulse (kırmızı, sarı, parlak renk) — kullanıcı arayüzünde

3. Performans sorunları:
   - width, height, top, left, margin, padding animasyonu
     (bunlar layout reflow tetikler — sadece transform ve opacity kullan)
   - JavaScript ile her frame manuel DOM manipülasyonu

4. Anlamsız dekorasyon:
   - Arka planda dönen geometrik şekiller
   - Köpük/parçacık efektleri (particle effects)
   - CSS 3D rotation arka planları

Örnek YASAK kod:
.card:hover { 
  box-shadow: 0 0 30px rgba(239,68,68,0.8); /* Kırmızı glow YASAK */
  animation: pulse 1s infinite;              /* Infinite pulse YASAK */
}
```

---

## 🎯 ANİMASYON KARAR AĞACI

Bir animasyon eklemeden önce şu soruları sor:

```
1. Bu animasyon kullanıcıya bilgi mi veriyor?
   → Evet: devam et
   → Hayır: EKLEME

2. Süre 500ms'den kısa mı?
   → Evet: devam et
   → Hayır: EKLEME (sadece progress fill 500ms alabilir)

3. GPU hızlandırmalı mı? (transform/opacity)
   → Evet: devam et
   → Hayır: EKLEME (layout/paint tetikleyen animasyon)

4. Kullanıcı prefers-reduced-motion tercihinde devre dışı bırakılıyor mu?
   → Evet: devam et (ZORUNLU)
   → Hayır: EKLEME
```

---

## ♿ ERİŞİLEBİLİRLİK (Reduced Motion)

```css
/* ZORUNLU: Tüm animasyonlarda bu blok bulunmalı */
@media (prefers-reduced-motion: reduce) {
  *,
  *::before,
  *::after {
    animation-duration: 0.01ms !important;
    animation-iteration-count: 1 !important;
    transition-duration: 0.01ms !important;
  }
}
```

---

## 📊 ANİMASYON PERFORMANS KURALLARI

```
✅ GPU Hızlandırmalı (kullan):
  transform: translateY(), translateX(), scale(), rotate()
  opacity: 0 → 1

❌ CPU Yoğun (kullanma):
  width, height değişimi
  top, left, margin, padding değişimi
  border-width değişimi

Doğru kullanım örneği:
.dropdown {
  opacity: 0;
  transform: translateY(-8px);
  pointer-events: none;
  transition: opacity 0.15s ease, transform 0.15s ease;
}
.dropdown.open {
  opacity: 1;
  transform: translateY(0);
  pointer-events: auto;
}
```
