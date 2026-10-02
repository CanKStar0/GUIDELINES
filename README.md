# 🧠 GUIDELINES: Universal AI Agent Constitution & Skill Hub

<p align="center">
  <a href="https://findfreeapi.com" target="_blank" rel="noopener noreferrer">
    <img src="https://findfreeapi.com/api/badge/developer?style=flat" alt="FreeAPI Verified Developer" />
  </a>
  <a href="https://findfreeapi.com" target="_blank" rel="noopener noreferrer">
    <img src="https://findfreeapi.com/api/badge/directory?style=flat" alt="FreeAPI Directory" />
  </a>
  <img src="https://img.shields.io/badge/Antigravity-Supported-4285F4?logo=google&logoColor=white" alt="Antigravity" />
  <img src="https://img.shields.io/badge/Cursor-Compatible-000000?logo=cursor&logoColor=white" alt="Cursor" />
  <img src="https://img.shields.io/badge/Claude_Code-Ready-D97706?logo=anthropic&logoColor=white" alt="Claude Code" />
  <img src="https://img.shields.io/badge/OpenAI_Codex-Compliant-10A37F?logo=openai&logoColor=white" alt="Codex" />
  <img src="https://img.shields.io/badge/License-MIT-blue.svg" alt="License MIT" />
</p>

> **Tek Kaynak (SSOT), Çoklu Platform ve Araç Bağımsız AI Agent Kuralları & Uzmanlık Kütüphanesi.**
>
> Projelerinizde hiçbir konfigürasyon çöplüğü (`.cursor/`, `.agents/skills/`, `.codex/` vb.) yaratmadan, tek bir `AGENTS.md` köprüsüyle tüm yapay zeka asistanlarınıza kıdemli yazılım mimarı personası ve doğrulanmış yetenekleri kazandırın.

---

## 🏛️ Mimari Felsefe (The Zero-Pollution Mandate)

Geleneksel yaklaşımlarda her yapay zeka aracı kendi klasörlerini (`.cursor/rules/`, `.agents/skills/`, `.vscode/`, `.github/copilot-instructions.md`) projenin içine doldurur ve proje dokümantasyon çöplüğüne döner. 

**GUIDELINES** mimarisi bu kirliliği tamamen ortadan kaldırır:

1. **Tek Kaynak (Single Source of Truth - SSOT):** Tüm anayasa kuralları ve uzmanlık becerileri bu merkezi depoda (`GUIDELINES`) tutulur.
2. **Sıfır Proje İçi Kirlilik (Zero-Pollution):** Geliştirme yaptığınız projeler içerisine asla yerel skill klasörleri kopyalanmaz veya commit edilmez.
3. **Tek Dosya Köprüsü (`AGENTS.md`):** Proje kök dizinine yalnızca tek bir temiz `AGENTS.md` dosyası bırakılır. Bu dosya, projenin teknoloji yığınını tanımlar ve gereken uzmanlıkları bu merkezi depodan dinamik olarak çeker.
4. **Çapraz Platform (OS & Tool Agnostic):** Windows, macOS ve Linux üzerinde; **Cursor, Claude Code, Antigravity, GitHub Copilot ve OpenAI Codex** ile %100 uyumlu çalışır.

---

## 📂 Dizin Yapısı

```text
GUIDELINES/
├── MASTER_AGENT_CONSTITUTION.md       # Sistem Personası, Hız Kuralları ve Genel AI Anayasası
├── PROJECT_AGENT_TEMPLATE.md          # Projeler için evrensel, çapraz platform AGENTS.md şablonu
├── PROJECT_AGENT_GENERATOR_PROMPT.txt # Projeyi salt-okunur tarayıp AGENTS.md üreten prompt
├── skills/                            # On-Demand (Gerektiğinde Yüklenen) Uzmanlık Yetenekleri
│   ├── master-orchestrator/           # Çoklu yetenek yönlendirme ve niyet dağıtıcısı
│   ├── bespoke-frontend-master/       # Özgün UI, semantik token'lar, a11y ve anti-slop kuralları
│   ├── resilient-backend-architect/   # Eşzamanlılık güvenliği, rate-limit, Zod doğrulama
│   ├── modern-data-engineer/          # Drizzle ORM, Prisma, PostgreSQL, pgvector & migration
│   ├── fullstack-security-auditor/    # OWASP Top 10, Auth/RBAC, sanitization ve DevSecOps
│   ├── ecommerce-payments-engine/     # Tamsayı kuruş matematiği, Stripe, Iyzico, sipariş state-machine
│   ├── seo-growth-architect/          # Teknik SEO, Schema JSON-LD, Core Web Vitals ve analitik
│   ├── autonomous-task-auditor/       # Otonom araştırma, dinamik self-audit ve self-healing
│   ├── superpowers-execution-harness/ # Çok dilli i18n, 4 sütunlu QA denetimi ve doğrulama kapıları
│   ├── create-design-md/              # 60-30-10 renk paletleri ve tasarım sistemi oluşturucu
│   ├── image-generation-studio/       # Sıfır metinli stüdyo aydınlatmalı görsel üretim yönergeleri
│   └── antigravity-guide/             # Google Antigravity, subagent ve arkaplan zamanlayıcı rehberi
└── README.md
```

---

## 🧩 Uzmanlık Yetenekleri Kataloğu (Skills)

| Yetenek (Skill) | Kapsam & Uzmanlık Alanı |
| :--- | :--- |
| **`master-orchestrator`** | Kullanıcı niyetini analiz eder, gerekli mimari yetenekleri dinamik olarak sıraya koyar ve koordine eder. |
| **`bespoke-frontend-master`** | Klişe ("AI-slop") arayüzleri engeller; projeye özel tipografi, semantik renk token'ları, mikro animasyonlar ve a11y standartları uygular. |
| **`resilient-backend-architect`** | Hata toleranslı, idempotent, Zod şemalı, rate-limit korumalı ve yüksek eşzamanlılığa dayanıklı backend mimarisi kurar. |
| **`modern-data-engineer`** | Drizzle ORM / Prisma veri modelleri, PostgreSQL indeksleme, migration stratejileri ve vektör (pgvector) boru hatları inşa eder. |
| **`fullstack-security-auditor`** | OWASP Top 10 kontrolleri, JWT/Session güvenliği, girdi temizleme, yetkilendirme (RBAC) ve gizli anahtar denetimi sağlar. |
| **`ecommerce-payments-engine`** | Finansal kayıpları önlemek için tamsayı kuruş (integer cents) hesabı, Stripe/Iyzico entegrasyonu ve stok rezervasyon döngüleri kurar. |
| **`seo-growth-architect`** | Sayfa hızı (Core Web Vitals), Schema.org JSON-LD yapılandırılmış verileri, OpenGraph ve semantik HTML optimizasyonu yapar. |
| **`autonomous-task-auditor`** | Yapılan değişiklikleri bağımsız olarak denetler, logları okur ve hata durumunda otonom düzeltme uygular. |
| **`superpowers-execution-harness`** | Çok dilli (i18n) projelerde eksik çeviri kontrolü, katı tip denetimi ve ampirik derleme/test kapılarını çalıştırır. |
| **`create-design-md`** | Proje için 60-30-10 kuralına dayalı, erişilebilir renk ve tipografi sözleşmesi (`DESIGN.md`) üretir. |
| **`image-generation-studio`** | E-ticaret ve UI için metinsiz, stüdyo ışıklı, izole ve yüksek çözünürlüklü görsel istemleri oluşturur. |
| **`antigravity-guide`** | Alt ajanlar (subagents), arka plan cron görevleri ve agent çalışma alanı kurallarını yönetir. |

---

## 🚀 Kurulum ve Kullanım

### 1. Depoyu Bilgisayarınıza Çekin
Bu repoyu bilgisayarınızda dilediğiniz bir yere clone'layın:
```bash
# Windows
git clone https://github.com/CanKStar0/GUIDELINES.git C:/GUIDELINES

# macOS / Linux
git clone https://github.com/CanKStar0/GUIDELINES.git ~/GUIDELINES
```

---

### 2. Projenizde Devreye Alın (Yalnızca Tek Adım)

Projenizin ana dizinine [PROJECT_AGENT_TEMPLATE.md](./PROJECT_AGENT_TEMPLATE.md) dosyasını **`AGENTS.md`** adıyla kopyalayın:

```markdown
# Developer Instructions (Proje Geliştirici & AI Anayasası)

<!-- DCM_GLOBAL_GUIDELINES_ROOT: /path/to/GUIDELINES -->

## 📌 Kapsam & Proje Tanımı
- **Proje:** MyAwesomeProject
- **Kök Dizin:** /path/to/project
- **Proje Amacı:** ...

## 🏛️ Merkezi Yetenek & Kural Referansı (SSOT)
- **Merkezi Anayasa:** <GLOBAL_GUIDELINES_ROOT>/MASTER_AGENT_CONSTITUTION.md
- **Global Yetenekler:** <GLOBAL_GUIDELINES_ROOT>/skills/

### Devreye Alınacak Global Yetenekler:
- Frontend & UI ➔ <GLOBAL_GUIDELINES_ROOT>/skills/bespoke-frontend-master/SKILL.md
- Backend & API ➔ <GLOBAL_GUIDELINES_ROOT>/skills/resilient-backend-architect/SKILL.md
- Güvenlik      ➔ <GLOBAL_GUIDELINES_ROOT>/skills/fullstack-security-auditor/SKILL.md
```

*(İsterseniz [PROJECT_AGENT_GENERATOR_PROMPT.txt](./PROJECT_AGENT_GENERATOR_PROMPT.txt) dosyasındaki promptu agent'ınıza vererek projenizin stack'ini otomatik analiz ettirip bu dosyayı 5 saniyede kendisinin oluşturmasını da sağlayabilirsiniz).*

---

### 3. Farklı Araçlarla Çalışma

* **Antigravity / Gemini CLI:** Proje kökündeki `AGENTS.md` dosyasını otomatik olarak algılar ve anayasayı yükler.
* **Cursor:** Kök dizindeki `AGENTS.md` dosyasını ana proje kuralı (System Prompt) olarak doğrudan işler.
* **Claude Code:** Terminalde `claude` komutunu başlattığınızda kökteki `AGENTS.md` dosyasını hafıza olarak okur.
* **GitHub Copilot / OpenAI Codex:** `AGENTS.md` endüstri standardı olduğu için yönergeleri otomatik bağlama dahil eder.

---

## 🌐 Geliştirici Ekosistemi & API Altyapısı

AI Agent'larınızla hızlı prototipleme yaparken, sahte veri oluştururken veya anahtarsız canlı REST API'lere ihtiyaç duyduğunuzda [FindFreeAPI.com](https://findfreeapi.com) dizininden faydalanabilirsiniz:

- **500+ Doğrulanmış Ücretsiz REST API:** [findfreeapi.com/explorer](https://findfreeapi.com/explorer)
- **Anahtarsız (No-Auth) Servisler:** API anahtarı beklemeden anında test edebileceğiniz uç noktalar.
- **Canlı Durum Rozetleri:** [findfreeapi.com/badge](https://findfreeapi.com/badge) üzerinden projeleriniz için dinamik SVG rozetleri.

---

## 📄 Lisans
Bu proje [MIT Lisansı](LICENSE) kapsamında açık kaynak olarak sunulmuştur.
