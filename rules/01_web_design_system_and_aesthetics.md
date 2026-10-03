# 🎨 MODERN WEB DESIGN SYSTEM & AESTHETICS GUIDELINES

> **TEMEL İLKE:** Tüm web uygulamalarında basmakalıp, çiğ veya jenerik görünen "AI-Slop" tasarımlar YASAKTIR. Arayüzler projenin kendi marka kimliğini, veri yoğunluğunu ve kullanıcı iş akışını kusursuz yansıtmalıdır.

---

## 🏛️ 1. PROJE-ÖNCELİKLİ TASARIM VE RENK İLKELERİ

1. **Mevcut Tasarım Sistemine Saygı:**
   - Projede tanımlı bir tema veya `DESIGN.md` varsa kesinlikle korunur. Rastgele yeni renk paleti veya stil dayatılamaz.
   - Ham fiziksel renkler (`#ffffff`, `bg-purple-600`, `text-slate-400`) bileşen içine gömülemez. Yalnızca projenin semantik token'ları (`bg-surface`, `text-muted`, `border-border`) tüketilir.

2. **Bağlamsal Köşe Yuvarlama (Border Radius Hierarchy):**
   - Tek tip 16–24px radius her yere zorla uygulanamaz.
   - Kontrollerde (buton/input) 6–8px, panellerde 8–12px, modallarda 12–16px tercih edilir. Yoğun terminal/geliştirici araçlarında 0px keskin köşeler tamamen meşrudur.

3. **Maksimum Veri Okunabilirliği ve Tipografi:**
   - Tablolarda, fiyatlarda, sayaçlarda ve KPI metriklerinde istisnasız `tabular-nums` uygulanır (rakamların genişlik atlamasını önler).
   - Başlıklarda `text-balance`, çok satırlı paragraflarda `text-pretty` kullanılır.

4. **Performanslı ve Amaca Yönelik Animasyonlar:**
   - Körlemesine `transition-all` kullanımı YASAKTIR. Sadece değişen özellik (`transition-colors`, `transition-opacity`, `transition-transform`) hedeflenir ve süre 200ms'yi aşmaz.
   - Yalnızca kompozitör özellikleri (`transform`, `opacity`) hareketlendirilir; `width`, `height`, `padding` animasyonu yasaktır.

---

## 🎯 2. SEMANTİK RENK VE DURUM STANDARTLARI

Durum renkleri projenin semantik token katmanından gelmelidir:
- **Başarı / Pozitif:** `--success` / `text-success` (veri durumları)
- **Hata / Tehlike:** `--destructive` (veya alias `--danger`) / `text-destructive`
- **Uyarı:** `--warning` / `text-warning`
- **Marka / Etkileşim:** `--primary` / `bg-primary` (sadece interaktif CTA ve aktif sekmeler; kart sınırlarına dekoratif olarak dağıtılmaz)
