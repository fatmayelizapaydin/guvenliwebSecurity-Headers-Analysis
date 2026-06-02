# 🛡️ Kurumsal Web Güvenliği Denetim Raporu: HTTP Güvenlik Başlıkları Analizi

**Denetim Tarihi:** 02.06.2026
**Denetçi:** Fatma Yeliz Apaydın
**Kapsam:** 10 Adet Web Uygulaması (Global ve Yerel Ölçekli)

---

## 1. Yönetici Özeti (Executive Summary)
Bu rapor, web uygulamalarının tarayıcı ile kurduğu güvenli iletişimi denetlemek amacıyla hazırlanmıştır. İncelenen 10 web sitesinin %60'ında, modern siber saldırılara (XSS, Clickjacking, MITM) karşı kullanılan HTTP başlıklarının ya eksik olduğu ya da yanlış yapılandırıldığı tespit edilmiştir.

## 2. Denetim Metodolojisi ve Tehdit Modeli
Denetim sürecinde **OWASP (Open Web Application Security Project)** rehberleri baz alınmıştır. Analiz, aşağıdaki **Saldırı Vektörü Matrisi** üzerinden yürütülmüştür:

| Saldırı Vektörü | Etki Düzeyi | Önleyici Başlık | Açıklama |
| :--- | :--- | :--- | :--- |
| **XSS** | Kritik | `Content-Security-Policy` | Zararlı script enjeksiyonlarını durdurur. |
| **Clickjacking** | Yüksek | `X-Frame-Options` | Sitenin iframe içinde kötüye kullanımını engeller. |
| **MITM** | Kritik | `Strict-Transport-Security` | İletişimi protokol seviyesinde şifreler. |
| **MIME Sniffing**| Orta | `X-Content-Type-Options` | Dosya tipinin tarayıcı tarafından manipülasyonunu keser. |



## 3. Saha Denetim Bulguları (10 Web Sitesi)
Analiz verileri, sistemli bir tarama (scan) çıktısıdır:

| Site | Skor | HSTS | CSP | X-Frame-Options | Risk Puanı |
| :--- | :---: | :---: | :---: | :---: | :---: |
| google.com | A+ | ✅ | ✅ | ✅ | 0/10 |
| facebook.com | A | ✅ | ✅ | ✅ | 1/10 |
| github.com | A | ✅ | ✅ | ✅ | 1/10 |
| wikipedia.org | B | ✅ | ❌ | ✅ | 3/10 |
| imdb.com | B | ✅ | ❌ | ✅ | 4/10 |
| n11.com | C | ✅ | ❌ | ❌ | 6/10 |
| sahibinden.com | C | ❌ | ❌ | ❌ | 7/10 |
| istinye.edu.tr | C | ❌ | ❌ | ✅ | 7/10 |
| hurriyet.com.tr | D | ❌ | ❌ | ❌ | 9/10 |
| milliyet.com.tr | D | ❌ | ❌ | ❌ | 9/10 |

## 4. Analiz ve İspat (PoC) Yaklaşımı
Her bir başlık eksikliği için **Proof of Concept (PoC)** uygulanmıştır. Örneğin; 
* **Clickjacking İspatı:** `X-Frame-Options` barındırmayan siteler, `<html><iframe src="https://hedef-site.com"></iframe></html>` koduyla bir iframe içine başarıyla gömülmüştür. 
* **XSS İspatı:** `Content-Security-Policy` eksikliği bulunan sitelerin tarayıcı konsoluna `alert(document.cookie)` komutu enjekte edilerek oturum verilerine erişilebileceği simüle edilmiştir.

---
*Bu çalışma, BGT208 Güvenli Web Yazılımı Geliştirme dersi kapsamında teknik denetim metodolojisiyle hazırlanmıştır.*
