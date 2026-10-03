# 09_multi_agent_qa_architecture.md

## 4-Agent (Böl ve Yönet) Test Mimarisi

Büyük projelerde (örn. MyDCM) tam doğruluk ve sıfır-hata QA testleri sağlamak için sistem aşağıdaki Çoklu-Ajan (Multi-Agent) mimarisiyle çalışır.

### 1. Rol Dağılımı ve Takımlar
Sistem iki ana takıma ayrılır (Müşteri ve Admin). Her takım kendi içinde bir "Görsel (Dedektif)" ve "Kod (Lider)" ajanı barındırır. Toplam 4 Subagent görev yapar:

- **Customer Team:** `Customer-Code-Inspector` (Lider) ve `Customer-UI-Inspector` (Dedektif)
- **Admin Team:** `Admin-Code-Inspector` (Lider) ve `Admin-UI-Inspector` (Dedektif)

### 2. Çift Konfigürasyon ve İzolasyon Prensibi
Ajanların ve oturumların birbirine karışmasını engellemek için projeler `projects/` altında izole edilir (örn. `mydcm-admin.json` ve `mydcm-customer.json`). Ajanlar asla kapsamı (scope) dışında bir rotayı analiz etmez.

### 3. Çevrimdışı (Offline Batch) Veri Kuralı
Ajanlar canlı site üzerinde eşzamanlı scraping YAPMAZ (Tarayıcı çakışmasını engellemek için).
1. Önce `qa-hunter.js` botu çalıştırılarak tüm hedef DOM ve Ekran Görüntüleri (Screenshots) `output/` dizinine çıkarılır.
2. 4-Ajan bu çevrimdışı (offline) klasörler üzerinde çalışır.

### 4. Lider ve Dedektif İletişim Protokolü
Ajanların sonsuz chat döngüsüne girmemesi için kesin bir protokol uygulanır:
1. **Dedektif (Visual Agent):** Görselleri inceler, sadece hataları tespit eder ve teknik bir rapor (Örn: "Kart taşması var") ile Lider Ajana mesaj atar.
2. **Lider (Code Agent):** Gelen görsel hata bildirimini kendi incelediği HTML/DOM kodları üzerinden doğrular, kök nedeni bulur (Örn: `CSS class eksik`) ve nihai Markdown özet raporunu (Örn: `changes_summary.md`) ana sisteme teslim eder.
