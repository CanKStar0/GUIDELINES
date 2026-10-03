# QA Fast Loop ve Agent Çalıştırma Protokolü

Bu dosya, BugHunter kullanan her insan geliştirici ve AI agent için zorunludur. Her yeni görevde kodu veya hedef projeyi incelemeden önce okunur.

## 1. Başlangıç kapısı — doküman okuma zorunluluğu

Her görev başlamadan önce:

1. Proje kökündeki `AGENTS.md` ve hedef projenin kendi `AGENTS.md` dosyaları okunur.
2. Hedef projedeki varsa `.agents/rules/` ve görevle ilgili özel kural dosyaları okunur.
3. Bu protokol, `docs/AGENT_QA_RUNBOOK.md` ve görsel/runtime işlerinde `.agents/skills/web-app-audit/SKILL.md` okunur.
4. Agent, okuduğu belgeleri görev notunda belirtir; belge okunmadıysa kod, komut veya mimari karar veremez.
5. İşin kapsamı belirlenir: günlük hızlı kontrol, değişen alan, görsel, etkileşim veya release denetimi.
6. Uygun QA profili seçilmeden rastgele `full` tarama başlatılmaz.
7. İkiden fazla adım varsa roadmap/state machine oluşturulur.
8. **Native Browser Audit (YENİ KURAL):** Ana agent (Antigravity), herhangi bir sayfa/UI geliştirme işlemini bitirdiğinde, offline betikler (qa-hunter.js) yerine **doğrudan tarayıcıyı kullanabilen `audit` subagent'ını** (`enable_mcp_tools: true` ile donatılmış) tetiklemekle yükümlüdür. Bu sayede testler direkt tarayıcı üzerinden, 4 Bütünlük Sütunu baz alınarak interaktif ve canlı yapılır.

## 2. Profil seçim matrisi

| Durum | Zorunlu profil | Komut |
|---|---|---|
| Her küçük kod değişikliği | `smoke` | `npm run qa:smoke -- --project=<proje>` |
| Belirli dosya/bileşen değişikliği | `affected` | `npm run qa:affected -- --project=<proje>` |
| CSS, responsive veya ekran değişikliği | `visual` | `npm run qa:visual -- --project=<proje>` |
| Buton, modal, form veya JS akışı | `interaction` | `npm run qa:interaction -- --project=<proje>` |
| Release / kullanıcıya teslim öncesi | `full` | `npm run qa:full -- --project=<proje>` |
| Yalnızca UX/ürün değerlendirmesi | `pm` | `npm run qa:pm -- --project=<proje>` |

MCP kullanan agent önce `get_qa_profiles`, gerçek test için `run_qa_profile` aracını kullanır. `run_visual_audit` tek başına gerçek runtime kanıtı üretmez; `NEEDS_RUNTIME_SCAN` sonucunu PASS olarak yorumlamak yasaktır.

## 3. Kanıt kapısı

Bir bulgu ancak aşağıdakiler birlikte sağlanıyorsa doğrulanmış kabul edilir:

- URL/final URL, viewport, selector ve selector eşleşme sayısı kayıtlıdır.
- Selector tam olarak tek elementi hedefler.
- Screenshot gerçekten dosyada vardır ve hedef element neon kırmızı-siyah halka ile işaretlenmiştir.
- Genel sayfa screenshot'ı alakasız bir hata için evidence olarak kullanılamaz.
- Tıklama sonucu tek başına hata onayı değildir; yeniden üretim veya gerçek network/DOM kanıtı gerekir.
- Belirsiz, flaky veya baseline farkı bulguları otomatik olarak onaylanmaz.

## 4. Cache, session ve baseline kuralları

- Smoke/affected cache kullanır; kaynak fingerprint değiştiğinde cache geçersiz sayılır.
- Session state tekrar kullanılabilir; giriş sorunu varsa `--fresh-session` ile sıfırlanır.
- Visual baseline yalnızca açıkça `--update-baseline` verilirse güncellenir ve eski baseline arşivlenir.
- Günlük hızlı tarama ile release taraması aynı şey değildir; release öncesi `full` çalıştırılır.

## 5. Görev kapanış kapısı

Agent şu dört çıktıyı görmeden “tamamlandı” demez:

1. `npm run build` çıkış kodu 0.
2. `npm test` çıkış kodu 0.
3. Seçilen QA profili gerçek runtime ile başarılı.
4. `output/<project>/audit-summary.json`, raporlar ve `changes_summary.md` güncel.

Sonuç kullanıcıya teknik satır listesiyle değil, `Önce / Sonra / Kullanıcı etkisi` diliyle aktarılır.
