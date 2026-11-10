---
name: seo-growth-architect
description: "Universal SEO & Growth Engine: Technical SEO, Core Web Vitals, Next.js metadata, JSON-LD Schema, Keyword Research & Clustering, AI/GEO Visibility, Competitor Gap, and GA4 DataLayer."
---

# 🔍 SEO & Growth Architect — 360° Arama Motoru, Yapay Zeka Görünürlüğü ve Teknik Büyüme Mimarisi

Bu yetenek; modern web uygulamalarında organik arama görünürlüğünü (Teknik SEO, Schema JSON-LD), yapay zeka arama motorlarındaki alıntılanabilirliği (AEO / GEO - AI Overviews, Perplexity, ChatGPT Search), anahtar kelime kümeleme mimarisini, Core Web Vitals performansını ve kurumsal analitik veri akışlarını (GA4 DataLayer) tek bir çatı altında yönetir.

Herhangi bir araca (OpenSEO, Semrush, Ahrefs, Search Console) bağımlı olmadan evrensel en iyi uygulamalarla çalışır.

---

# 🚫 KESİN YASAKLAR — UNFORGIVABLE SEO ANTI-PATTERNS

1. **İstemci Taraflı (CSR) Metadata Yasaktır:**
   - Sayfa başlıkları, açıklamaları ve OpenGraph etiketleri `useEffect` ile istemcide basılamaz. Mutlaka sunucu tarafında (Next.js `generateMetadata` veya SSR) render edilmelidir.
2. **Boyutsuz Görsel Etiketleri Yasaktır:**
   - Genişlik (`width`), yükseklik (`height`) veya CSS `aspect-ratio` belirtilmemiş ham `<img>` etiketleri yasaktır (CLS > 0.1 patlamasına yol açar). `next/image` veya rezerve edilmiş kapsayıcılar kullanılmalıdır.
3. **Temiz Olmayan URL Yapıları Yasaktır:**
   - Büyük harf, boşluk (`%20`), özel karakter veya alt tire içeren URL'ler yasaktır. Daima küçük harf ve tireli temiz slug'lar kullanılmalıdır: `/products/ai-terminal-v2`.
4. **Tek Yönlü Hreflang Yasaktır:**
   - Çoklu dil yapılarında A dilinden B diline bağlantı veriliyorsa, B dilinden de A diline karşılıklı (`bidirectional`) ve `x-default` içeren alternatif etiketleri zorunludur.
5. **Arama Motorlarını CSS/JS Varlıklarında Engellemek Yasaktır:**
   - `robots.txt` içinde `/_next/` veya static asset'leri disallow etmek yasaktır. Botların sayfayı görsel ve düzen olarak doğru render edebilmesi için CSS/JS açık bırakılmalıdır.
6. **Anahtar Kelime Yamyamlığı (Keyword Cannibalization):**
   - Aynı ana anahtar kelimeyi ve aynı arama niyetini hedefleyen birden fazla sayfa üretmek yasaktır. Her ana niyet tek bir yetkili sayfaya (`canonical intent URL`) bağlanmalıdır.

---

# 🏛️ 1. TEKNİK SEO, SCHEMA & METADATA STANDARTLARI

### A. Dinamik `sitemap.xml` & `robots.txt`
```text
User-agent: *
Allow: /
Disallow: /api/
Disallow: /admin/
Disallow: /checkout/
Disallow: /*?*sort=

Sitemap: https://www.example.com/sitemap.xml
```

### B. Modern Next.js 15+ Metadata & Hreflang Şablonu

```typescript
import type { Metadata } from "next";

// Statik Sayfa Örneği
export const metadata: Metadata = {
  title: "AI Finance Terminal | Gerçek Zamanlı Piyasa Analizi",
  description: "Finansal piyasaları derinlemesine analiz edin, veriye dayalı kararlar alın.",
  alternates: {
    canonical: "https://www.example.com/products/ai-terminal",
    languages: {
      en: "https://www.example.com/en/products/ai-terminal",
      tr: "https://www.example.com/tr/products/ai-terminal",
      "x-default": "https://www.example.com/en/products/ai-terminal",
    },
  },
  openGraph: {
    type: "website",
    title: "AI Finance Terminal | Gerçek Zamanlı Piyasa Analizi",
    description: "Finansal piyasaları derinlemesine analiz edin.",
    images: [{ url: "https://www.example.com/assets/og-cover.jpg", width: 1200, height: 630 }],
  },
  twitter: {
    card: "summary_large_image",
  },
};

// Dinamik Rotalar (Next.js 15+ App Router: params asenkron Promise'dir)
export async function generateMetadata({ params }: { params: Promise<{ slug: string }> }): Promise<Metadata> {
  const { slug } = await params;
  return {
    title: `${slug.toUpperCase()} | Piyasa Analizi`,
    alternates: {
      canonical: `https://www.example.com/products/${slug}`,
    },
  };
}
```

### C. Yapılandırılmış Veri (Schema.org JSON-LD)
Arama motorları ve LLM'lerin varlık ilişkilerini (entity graph) kurabilmesi için temiz JSON-LD:

```json
{
  "@context": "https://schema.org",
  "@graph": [
    {
      "@type": "Organization",
      "@id": "https://www.example.com/#organization",
      "name": "DCM Development",
      "url": "https://www.example.com",
      "logo": "https://www.example.com/assets/logo.png"
    },
    {
      "@type": "WebSite",
      "@id": "https://www.example.com/#website",
      "url": "https://www.example.com",
      "name": "DCM Development",
      "publisher": { "@id": "https://www.example.com/#organization" },
      "potentialAction": {
        "@type": "SearchAction",
        "target": "https://www.example.com/search?q={search_term_string}",
        "query-input": "required name=search_term_string"
      }
    }
  ]
}
```

---

# 🎯 2. ANAHTAR KELİME ARAŞTIRMASI & NİYET KÜMELEME (KEYWORD CLUSTERING)

Arama niyeti (Search Intent) doğru anlaşılmadan üretilen hiçbir içerik sıralama alamaz.

### A. Arama Niyeti Sınıflandırması
1. **Bilgi Odaklı (Informational - "Nedir / Nasıl"):** Rehberler, dokümanlar, kavram açıklamaları. Hedef: Güven kazanma, üst huni (top of funnel).
2. **Araştırma / Karşılaştırma (Commercial Investigation - "En İyi / Alternatifler"):** "En iyi CRM araçları", "A vs B karşılaştırması". Hedef: Değerlendirme aşaması.
3. **İşlem Odaklı (Transactional - "Satın Al / Fiyat / İndir"):** Ürün ve ödeme sayfaları, pricing tabloları. Hedef: Dönüşüm.
4. **Gezinme Odaklı (Navigational - Marka Aramaları):** Doğrudan marka ismi veya login sayfaları.

### B. Hub & Spoke (Pillar-Cluster) Sayfa Mimarisi
- **Pillar (Hub) Sayfa:** Geniş kapsamlı ana konu (Örn: `/seo-rehberi/`).
- **Cluster (Spoke) Sayfalar:** Alt konuları derinlemesine ele alan spesifik sayfalar (Örn: `/seo-rehberi/teknik-seo/`, `/seo-rehberi/schema-markup/`).
- **İç Linkleme (Internal Linking):** Her spoke sayfası doğrudan ait olduğu pillar sayfaya link vermeli; benzer spoke sayfalar ise yatayda birbirine bağlamlı linklerle otorite aktarmalıdır.

---

# 🤖 3. YAPAY ZEKA ARAMA VE GÖRÜNÜRLÜK (AEO & GEO MİMARİSİ)

Google AI Overviews, Perplexity, ChatGPT Search ve Gemini gibi LLM tabanlı arama motorlarında kaynak gösterilmek ve önerilmek için:

1. **Doğrudan ve Net Cevap Formatı (Answer First):**
   - Başlıktan hemen sonraki ilk 2 cümlede konunun özü (definition/answer) doğrudan verilmelidir. LLM özetleyiciler doğrudan bu ilk paragrafları alıntılar.
2. **Faktoid ve Yapılandırılmış Veri Yoğunluğu:**
   - Tablolar, madde işaretleri, net istatistikler ve doğrulanabilir veriler metin yığınlarından çok daha yüksek alıntılanma oranına sahiptir.
3. **Varlık Netliği (Entity Clarity):**
   - Şirket, kurucu, ürün ve kategori isimleri sitede tutarlı olarak geçmeli; `Organization` ve `Product` schemaları ile resmi sosyal profillere (`sameAs`) bağlanmalıdır.
4. **Soru-Cevap & SSS Blokları:**
   - Sayfa sonlarında `FAQPage` schemasıyla zenginleştirilmiş, kullanıcıların en sık sorduğu 3–5 kritik soru ve kısa net cevapları bulunmalıdır.

---

# 📊 4. RAKİP ANALİZİ & İÇERİK AÇIĞI (CONTENT GAP)

Organik pazarda liderlerle rekabet ederken izlenecek adımlar:

1. **SERP İlk 10 Analizi:**
   - Hedeflenen anahtar kelimede Google ilk 10 sonucunun sayfa türünü incele: Kullanıcı rehber mi istiyor, interaktif hesap makinesi mi, yoksa e-ticaret listesi mi? Yanlış sayfa formatıyla doğru içerik üretilemez.
2. **Ortak Sıralama Boşlukları (Keyword Gap):**
   - Rakiplerin ilk 20'de yer alıp bizim sitemizin hiç sıralanmadığı yüksek hacimli terimleri tespit et.
3. **Otorite ve Backlink Boşluğu:**
   - Rakiplerin hangi sektör rehberlerinden, açık kaynak listelerinden veya haber sitelerinden link aldığını haritalandır; benzer veya daha kapsamlı bir kaynak üreterek doğal bağlantı kazan.

---

# 📍 5. YEREL SEO VE HARİTA GÖRÜNÜRLÜĞÜ (LOCAL SEO)

Fiziksel konuma veya yerel hizmet alanına bağlı projeler için:

1. **NAP Tutarlılığı (Name, Address, Phone):**
   - İşletme adı, açık adresi ve telefon numarası web sitesi altbilgisinde (footer), iletişim sayfasında ve Google Business Profile üzerinde birebir aynı karakterlerle yer almalıdır.
2. **`LocalBusiness` Schema:**
   - Çalışma saatleri, coğrafi koordinatlar (`geo`), kabul edilen ödeme yöntemleri ve hizmet bölgesi JSON-LD ile işaretlenmelidir.
3. **Yerel Açılış Sayfaları (Local Landing Pages):**
   - Çoklu şube veya bölgeye hizmet veriliyorsa `/istanbul/kadikoy/` gibi her bölge için özgün içerikli, yerel referanslar içeren alt sayfalar kurgulanmalıdır.

---

# ⚡ 6. CORE WEB VITALS & CONVERSION RATE OPTIMIZATION (CRO)

- **LCP (Largest Contentful Paint < 2.5s):** Hero görseli ve kritik kat üstü (above-the-fold) bileşenlerde `priority={true}` ve WebP/AVIF formatı.
- **CLS (Cumulative Layout Shift < 0.1):** Tüm dinamik banner ve reklam alanlarında önceden sabit yükseklik (`min-h-[...]`) tanımlama.
- **INP (Interaction to Next Paint < 200ms):** Tıklamalarda ana iş parçacığını kilitleyen ağır JavaScript döngülerinden kaçınma.

### Standartlaştırılmış GA4 / GTM DataLayer Akışı:
```typescript
export function trackDataLayerEvent(event: string, payload: Record<string, any>) {
  if (typeof window !== "undefined") {
    window.dataLayer = window.dataLayer || [];
    window.dataLayer.push({ event, ...payload, timestamp: Date.now() });
  }
}
```
