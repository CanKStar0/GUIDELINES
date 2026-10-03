# 🧠 Hafıza, Bağlam & Halüsinasyon Önleme Standartları (Smart Context & Pruning)

> **Amaç:** AI bağlamının (context window) gereksiz geçmiş sohbet loglarıyla şişmesini önlemek, bayat veri ezberleme halüsinasyonunu sıfırlamak ve token israfını engellemek.

---

## ⚡ 1. DÖRT KATMANLI AKILLI BAĞLAM HİYERARŞİSİ (4-TIER CONTEXT)

Ajan her turda tüm sohbet geçmişini tekrar tekrar okumak yerine şu 4 katmanlı disiplinle çalışır:

1. **Katman 1: Güncel İntent & Anlık Döngü (Son 2-3 Mesaj):**
   - Sadece kullanıcının son komutuna ve hemen önceki 1-2 takip mesajına odaklan. Eski konuşma loglarını ezberleme.
2. **Katman 2: Aktif Proje Durumu (State / Artifacts):**
   - Projenin aktif mimari kararları ve ilerleme durumu `output/roadmap.json` veya `implementation_plan.md` üzerinden 10-15 satırlık özetle takip edilir.
3. **Katman 3: Tek Gerçek Kaynak (Diskteki Canlı Kod - Disk as SSOT):**
   - Sohbette geçmişte paylaşılmış eski kod bloklarını "canlı kod" sanmak KESİNLİKLE YASAKTIR.
   - Her zaman `view_file` ile **diskteki en güncel fiziksel dosyayı** oku.
4. **Katman 4: İhtiyaç Anında Yüklenen Uzmanlıklar (On-Demand Skills):**
   - Tüm kuralları hafızada tutmak yerine sadece ilgili `SKILL.md` dosyasını `view_file` ile oku.

---

## 📏 2. HAFIZA & DERS YÖNETİM KURALLARI (HERMES MEMORY)

1. **Sıkı Boyut Sınırı (Max 10 Madde / 150 Token - FIFO):**
   - Hafıza dosyaları (`output/<project>/memory.json`) asla ham log çöplüğü olamaz.
   - Maksimum **10 ders/madde** barındırabilir. 11. kural geldiğinde en eski kayıt silinir (FIFO).
2. **Kural Birleştirme (Consolidation):**
   - Benzer hatalar tek bir birleşik kurala indirgenir.
   - ❌ *Eski:* "Sayfa A'da 14px unutuldu", "Sayfa B'de 12px unutuldu"
   - 🟢 *Yeni:* "Tüm mobil form girdilerinde zoom engellemek için minimum `16px` font zorunludur."
3. **Proje Bazlı İzole Hafıza:**
   - Bir projedeki mimari karar veya kütüphane tercihi başka bir projeye bulaştırılamaz.
