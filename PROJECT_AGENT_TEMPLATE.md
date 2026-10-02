# Developer Instructions (Proje Geliştirici & AI Anayasası)

<!-- DCM_GLOBAL_GUIDELINES_ROOT: <GLOBAL_GUIDELINES_ROOT> -->

## 📌 Kapsam & Proje Tanımı
- **Proje:** `<PROJECT_NAME>`
- **Kök Dizin:** `<PROJECT_ROOT>`
- **Proje Amacı:** <Kısa, net ve kanıtlanmış proje amacı ve hedef kitlesi>

---

## 🏛️ Merkezi Yetenek & Kural Referansı (SSOT)

Bu projede çalışırken tüm temel kurallar ve uzmanlıklar aşağıdaki merkezi kütüphaneden okunur. Proje içinde gereksiz yerel skill klasörleri (.codex, .agents/skills vb.) barındırılmaz.

> 🧭 **Yol Çözümleme (Cross-Platform Path Resolution):**
> `<GLOBAL_GUIDELINES_ROOT>` değeri; yerel ortamdaki `GUIDELINES` reposunun mutlak veya göreceli yoludur (Örn. Windows: `C:/Users/<Kullanıcı>/Desktop/GUIDELINES` veya `D:/GUIDELINES`, macOS/Linux: `~/GUIDELINES` veya komşu dizin `../GUIDELINES`). Tüm araçlar (Antigravity, Cursor, Claude Code, Codex) evrensel düz taksim (`/`) yolunu tanır.

- **Merkezi Anayasa:** `<GLOBAL_GUIDELINES_ROOT>/MASTER_AGENT_CONSTITUTION.md`
- **Global Yetenekler:** `<GLOBAL_GUIDELINES_ROOT>/skills/`

### Proje İhtiyacına Göre Devreye Alınacak Başlıca Global Yetenekler:
- `<Görev Alanı>` ➔ `<GLOBAL_GUIDELINES_ROOT>/skills/<global-skill>/SKILL.md`
- `<Görev Alanı>` ➔ `<GLOBAL_GUIDELINES_ROOT>/skills/<global-skill>/SKILL.md`

---

## 🛠️ Doğrulanmış Teknoloji Yığını (Tech Stack)

- **Dil / Çalışma Zamanı:** `<...>`
- **Framework / Platform:** `<...>`
- **Veritabanı / ORM:** `<...>`
- **Frontend / UI:** `<...>`
- **Paket & Derleme Araçları:** `<...>`
- **Test Araçları:** `<...>`

---

## 🔒 Güvenlik & Mimari Kuralları

- `<Doğrulanmış mimari kurallar>`
- `<Yetkilendirme ve veri güvenliği kuralları>`
- Asla hassas API anahtarlarını, token'ları veya gizli verileri loglara veya açık kaynak koduna yazma.

---

## ⚡ Doğrulama Komutları (Verification Commands)

Yapılan değişikliklerden sonra çalıştırılacak ampirik test ve build komutları:

```bash
<build veya test komutu>
```
