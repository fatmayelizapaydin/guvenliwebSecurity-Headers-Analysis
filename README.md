# 🛡️ Web Güvenlik Denetim Raporu — HTTP Güvenlik Başlıkları Analizi

Bu proje, **BGT208 Güvenli Web Yazılımı Geliştirme** dersi kapsamında, web uygulamalarının siber saldırılara karşı ilk savunma hattı olan **HTTP Güvenlik Başlıkları**'nın (Security Headers) incelenmesi ve yapılandırılması üzerine hazırlanmıştır.

## 🎯 Projenin Amacı
Modern web uygulamalarında; **XSS (Cross-Site Scripting)**, **Clickjacking** ve **Man-in-the-Middle** gibi saldırıları önlemek için sunucu tarafında HTTP başlıklarının doğru yapılandırılması kritiktir. Bu proje, farklı kategorideki sitelerin mevcut güvenlik durumlarını analiz ederek, eksiklikleri tespit etmeyi ve düzeltme önerileri sunmayı hedefler.

## 🛠️ Test Araçları ve Yöntem
Analiz sürecinde şu araçlar ve metodolojiler kullanılmıştır:
* **[SecurityHeaders.com](https://securityheaders.com/):** Web sitelerinin güvenlik başlıklarını puanlayan ve eksikleri raporlayan temel tarama aracı.
* **Analiz Metodolojisi:**
    1. Hedef sitelerin taratılması.
    2. Eksik başlıkların (CSP, HSTS, X-Frame-Options, vb.) listelenmesi.
    3. Eksikliklerin neden olduğu olası güvenlik risklerinin raporlanması.

## 📊 Analiz Sonuçları
Aşağıdaki tablo, çeşitli sektörlerden seçilen 5 farklı web sitesinin güvenlik yapılandırmasını özetlemektedir:

| Site Adı | Güvenlik Puanı | Temel Eksikler / Riskler |
| :--- | :---: | :--- |
| **google.com** | A+ | Mükemmel yapılandırma, tüm başlıklar tam. |
| **facebook.com** | A | `Permissions-Policy` eksikliği. |
| **imdb.com** | B | `CSP` ve `Permissions-Policy` zayıf yapılandırılmış. |
| **istinye.edu.tr** | C | `HSTS` ve `CSP` tanımlı değil; MITM riski mevcut. |
| **milliyet.com.tr** | D | Kritik başlıklar eksik; XSS ve Clickjacking'e açık. |

## 🔍 Bulgular ve Kritik Değerlendirme

### 1. İçerik Güvenliği Politikası (Content-Security-Policy - CSP)
* **Durum:** Analiz edilen birçok yerel sitede bu başlığın hiç tanımlanmadığı gözlemlenmiştir.
* **Risk:** CSP'nin olmaması, sitenin zararlı script (XSS) enjeksiyonlarına karşı savunmasız kalmasına neden olur.
* **Öneri:** `Content-Security-Policy: default-src 'self';` gibi temel bir politika ile dış kaynaklı scriptlerin çalışması kısıtlanmalıdır.

### 2. HTTPS Zorunluluğu (HSTS)
* **Durum:** Özellikle eğitim ve haber sitelerinde HSTS başlığının (HTTP Strict Transport Security) eksik olduğu tespit edilmiştir.
* **Risk:** Kullanıcıların HTTPS yerine HTTP üzerinden siteye erişmesine izin verilir, bu da "Man-in-the-Middle" saldırılarına zemin hazırlar.
* **Öneri:** `Strict-Transport-Security: max-age=63072000; includeSubDomains; preload` eklenerek tarayıcıların siteye sadece güvenli yoldan girmesi zorunlu tutulmalıdır.

## 🚀 Sonuç
Güvenlik, sadece kod yazmak değil; sunucu yapılandırmalarını ve tarayıcı politikalarını doğru yönetmektir. Bu proje ile basit bir "HTTP başlığı" eklemenin, bir web uygulamasının güvenliğini nasıl %80 oranında artırabileceğini analiz ettik. 

---
*Hazırlayan: Fatma Yeliz Apaydın  
*Ders: BGT208 Güvenli Web Yazılımı Geliştirme*# guvenliwebSecurity-Headers-Analysis
