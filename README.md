# 🧠 GUIDELINES: Universal AI Agent Constitution & Skill Hub

Merkezi, çoklu platform (Cross-Platform) ve araç bağımsız (Cursor, Claude Code, Antigravity, OpenAI Codex) AI Agent kuralları, anayasası ve uzmanlık yetenekleri (Skills).

---

## 🏛️ Mimari & Felsefe (Zero-Pollution & SSOT)

Bu repo, tüm projelerde sıfır kirlilik prensibiyle çalışmak üzere tasarlanmıştır:
1. **Tek Kaynak (SSOT):** Tüm anayasa ve uzmanlık kuralları bu merkez depoda yaşar.
2. **Sıfır Kirlilik (Zero Pollution):** Projeler içinde gereksiz klasör çöplüğü (`.cursor/`, `.agents/skills/`, `.codex/` vb.) oluşturulmaz.
3. **Tek Dosya Köprüsü (`AGENTS.md`):** Proje kök dizininde yer alan tek bir `AGENTS.md` dosyası, projenin mimarisini ve ihtiyaç duyduğu merkezi yetenekleri buradaki dosyalara bağlar.

---

## 📂 Dizin Yapısı

```text
GUIDELINES/
├── MASTER_AGENT_CONSTITUTION.md       # Ana AI Anayasası ve Sistem Personası
├── PROJECT_AGENT_TEMPLATE.md          # Projeler için evrensel AGENTS.md şablonu
├── PROJECT_AGENT_GENERATOR_PROMPT.txt # Projeleri tarayıp AGENTS.md üreten prompt
├── skills/                            # Uzmanlaşmış Agent Yetenekleri
│   ├── bespoke-frontend-master/
│   ├── resilient-backend-architect/
│   ├── modern-data-engineer/
│   ├── fullstack-security-auditor/
│   ├── ecommerce-payments-engine/
│   ├── seo-growth-architect/
│   ├── autonomous-task-auditor/
│   ├── superpowers-execution-harness/
│   ├── create-design-md/
│   ├── image-generation-studio/
│   └── antigravity-guide/
└── README.md
```

---

## 🚀 Yeni Bir Projede Nasıl Kullanılır?

1. Bu repoyu bilgisayarında dilediğin bir konuma clone'la (Örn: `~/GUIDELINES` veya `C:/GUIDELINES`).
2. Yeni projene başlarken [PROJECT_AGENT_GENERATOR_PROMPT.txt](./PROJECT_AGENT_GENERATOR_PROMPT.txt) içeriğini agent'ına ver veya [PROJECT_AGENT_TEMPLATE.md](./PROJECT_AGENT_TEMPLATE.md) şablonunu projenin köküne `AGENTS.md` adıyla kopyala.
3. `<GLOBAL_GUIDELINES_ROOT>` alanına bu reponun bilgisayarındaki yolunu belirt.
4. **Cursor, Claude, Antigravity veya Codex** projeyi açtığı anda tüm kuralları ve yetenekleri otomatik olarak uygular.
