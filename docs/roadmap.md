# 🗺️ ROADMAP — Web Uygulamaları Güvenlik Konfigürasyon Denetimi

> **Course / Ders:** Secure Web Development (BGT208) · Istinye University
> **Instructor / Danışman:** Keyvan Arasteh

---

## Phase 0 / Faz 0: Understand Before You Build / Yazmadan Önce Anla
- **Proje:** 10 web sitesinin güvenlik başlıkları (Security Headers) analizi ve sıkılaştırma (hardening).
- **Çalışma:** HTTP response başlıklarını tarayıcı araçları ve `SecurityHeaders.com` üzerinden denetlemek.
- **Araçlar:** Chrome DevTools, `curl`, `SecurityHeaders.com`, Nginx konfigürasyonları.

---

## Phase 1 / Faz 1: Research & Investigation / Araştırma ve Keşif
> Folder / Klasör: `docs/research/`

| Topic / Konu | Status / Durum | Notes / Notlar |
|--------------|----------------|----------------|
| HTTP Security Headers | ✅ Completed | XSS, HSTS, CSP analizi tamamlandı. |
| Vulnerability Research | ✅ Completed | Clickjacking ve MITM riskleri incelendi. |
| Site Benchmarking | ✅ Completed | 10 popüler web sitesi tarandı. |

---

## Phase 2 / Faz 2: Environment Setup / Ortam Kurulumu
- [x] Isolated lab environment (Localhost/Cloud)
- [x] Tools installed and verified (Terminal/DevTools)
- [x] Security Audit structure created

---

## Phase 3 / Faz 3: Implementation / Uygulama
### Module / Modül: Server Hardening

1. **Adım 1:** Nginx güvenlik konfigürasyon dosyası oluşturuldu.
2. **Adım 2:** CSP ve HSTS politikaları "strict" seviyeye çekildi.
3. **Adım 3:** Middleware (helmet) kullanımı ile uygulama seviyesinde koruma sağlandı.

---

## Phase 4 / Faz 4: Testing & Reporting / Test ve Raporlama
- [x] Ran tests against 10 target sites
- [x] Documented all findings with evidence (PoC reports)
- [x] Wrote final report (Markdown documentation)

---

## Phase 5 / Faz 5: Delivery / Teslim
- [x] GitHub repository is clean and organized
- [x] README.md complete
- [x] Instructor invited as collaborator → **keyvanarasteh**

---

## What I Learned / Öğrendiklerim
* **Ne zordu?** Farklı web sitelerinin güvenlik politikalarındaki tutarsızlıkları analiz edip standart bir puanlama sistemine oturtmak zorlayıcıydı.
* **Ne şaşırttı?** Global ölçekte bile birçok platformun temel güvenlik başlıklarını (HSTS gibi) atladığını görmek oldukça şaşırtıcıydı. Güvenliğin sadece kodda değil, sunucu konfigürasyonunda başladığını bizzat deneyimledim.
