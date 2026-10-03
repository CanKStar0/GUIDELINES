# 📱 Mobile & iOS Safari WebKit Standartları

> 💡 **Bu dosya sadece Mobil / Responsive Arayüz geliştirme ve hata düzeltmelerinde geçerlidir.**

1. **Form Input Auto-Zoom Engelleme:**
   - Mobil görünümde (`@media (max-width: 768px)`), tüm `input`, `select`, `textarea`, `.admin-input` ve `.site-input` elemanlarında font boyutu kesinlikle `16px !important;` (`touch-action: manipulation;`) olarak korunur. 16px altı font boyutlarının iOS Safari'de sayfayı otomatik yakınlaştırması (auto-zoom) engellenir.

2. **Form ve Taşıyıcı Genişlik Güvenliği:**
   - Mobil form ve input kapsayıcılarında (`.site-form`, `.site-input`, `.site-select`, `.site-textarea`) `width: 100%; max-width: 100%; box-sizing: border-box; min-width: 0; word-break: break-word; overflow-wrap: break-word;` kuralları zorunludur. Çekirdek form elemanları yatay taşma yapamaz. Checkbox ve radyo butonlarında `flex-shrink: 0` kullanılır.

3. **iOS WebKit Body Fixed Position Scroll Locking:**
   - Modallar (Oyuncu Profili Modal, Mobil Menü vb.) açıldığında `body` üzerine `position: fixed; top: -scrollYpx; width: 100%;` atanarak iOS rubber-band arka plan kayması engellenir. Modal kapatıldığında `document.activeElement.blur()` ile dokunmatik odak sıfırlanır, `position` kaldırılır ve `window.scrollTo(0, savedScrollY)` ile sayfa scroll konumu kusursuz geri yüklenir.

4. **Global WebKit `[hidden]` Kuralı:**
   - Tüm CSS yapılarında `[x-cloak], [hidden] { display: none !important; }` kuralı zorunludur. iOS WebKit motorunun `hidden` olan grid ögelerini veya scroll oklarını hatalı konumlandırması engellenir.
