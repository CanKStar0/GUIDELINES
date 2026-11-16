# Tarayıcı Otomasyonu: `browsermcp` vs Yerleşik `browser` Subagent Ayrımı

## Temel İlke
İki tarayıcı aracı görev kapsamına göre birbirini tamamlar; çakışma yaşamamak için aşağıdaki net sınırlar uygulanır:

## Ne Zaman `browsermcp` Kullanılır?
- Kullanıcının halihazırda oturum açmış olduğu veya aktif Chrome sekmelerinde işlem yapılacağı durumlarda (Cloudflare, Vercel, Dokploy, Supabase, Google Cloud, Gmail, Analytics, GitHub, Admin panelleri).
- Kullanıcı açıkça *"benim tarayıcımda / açık sekmede / browsermcp ile yap"* dediğinde.
- İlk çağrıda `<appDataDir>\mcp\browsermcp\browser.json` şeması okunup `call_mcp_tool` ile işlem yürütülür.

## Ne Zaman Yerleşik `browser` Subagent Kullanılır?
- `localhost:PORT` önizlemeleri, bağımsız görsel QA testleri, genel web sayfası gezintisi ve temiz/izole (anonim) oturum gerektiren UI iş akışlarında (Antigravity sistem yönergesi gereği ilk turda doğrudan `browser` subagent'a devredilir).
- `browsermcp` eklentisi bağlı değilse veya erişilemiyorsa fallback olarak.
