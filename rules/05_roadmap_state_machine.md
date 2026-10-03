# 🗺️ DYNAMIC ROADMAP & STATE MACHINE PROTOCOL

> **ZORUNLU KURAL:** Çok adımlı (2'den fazla adımı olan) hiçbir görev doğrudan koda dökülemez veya sadece metin planı ile bırakılamaz. Projenin canlı `.agent/roadmap.json` durum dosyası oluşturulmalı ve her adım ampirik doğrulama ile güncellenmelidir.

---

## 🏛️ 1. MİMARİ VE STATE MACHINE AKIŞI

Karmaşık ve çok adımlı görevlerde ilerleme durumu atomik adımlara bölünür ve projenin durum dosyasında (`output/roadmap.json` veya `implementation_plan.md` plan artifact'i) bir **State Machine** olarak takip edilir.

### Adım Statüleri:
- **`pending`**: Bekleyen adım.
- **`in_progress`**: Şu an yürütülen aktif adım.
- **`completed`**: Ampirik doğrulama (Exit Code 0) ile başarıyla tamamlanan adım.
- **`failed`**: Komut veya test başarısız oldu (deneme sayısı 1 artar).
- **`stuck`**: Adım 3 kez üst üste başarısız oldu (`attempts >= 3`). Sistem kilitlenir ve geliştiriciden/kullanıcıdan müdahale talep eder.

---

## 🛠️ 2. KULLANIM YÖNTEMİ
1. Göreve başlamadan önce adımlar belirlenir ve plana dökülür.
2. Her adım tamamlandığında ampirik komut (build/test) ile doğrulanıp `completed` statüsüne alınır.
3. Otomasyon scriptleri bulunan projelerde (`scripts/roadmap-cli.js` veya MCP) yerel CLI kullanılabilir; bulunmayan projelerde durum plan artifact'i üzerinden güncellenir.

---

## 🛑 3. STUCK (KİLİTLENME) VE KURTARMA PROTOKOLÜ

Bir adım 3 defa başarısız olduğunda (`attempts >= 3`), statü otomatik olarak **`stuck`** olur. 
AI Agent bu durumda durmalı, hata nedenlerini ve log çıktılarını kullanıcıya açık bir özetle raporlamalıdır.
