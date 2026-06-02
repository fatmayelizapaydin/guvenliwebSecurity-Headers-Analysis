# # 🛡️ Web Uygulamaları Güvenlik Konfigürasyon Denetimi (Pentest-Audit)

**Hazırlayan:** Fatma Yeliz Apaydın  
**Ders:** BGT208 Güvenli Web Yazılımı Geliştirme

## 1. Projenin Amacı
Bu çalışma, web uygulamalarının siber saldırılara karşı ilk savunma hattı olan **HTTP Güvenlik Başlıkları'nın (Security Headers)** analizini ve yapılandırmasını konu almaktadır. 10 farklı popüler web sitesi üzerinden gerçekleştirilen bu denetim, modern web saldırılarına (XSS, MITM, Clickjacking) karşı sunucu tarafındaki zafiyetleri ortaya koymayı hedefler.

## 2. 10 Popüler Web Sitesi Güvenlik Denetim Raporu
Aşağıdaki siteler, `SecurityHeaders.com` standartları baz alınarak analiz edilmiştir:

| Site Adı | Skor | Kritik Eksiklik / Zayıflık |
| :--- | :---: | :--- |
| **google.com** | A+ | - (Tüm başlıklar optimize) |
| **facebook.com** | A | `Permissions-Policy` zayıf |
| **github.com** | A | `Permissions-Policy` eksikliği |
| **wikipedia.org**| B | `CSP` ve `Permissions-Policy` yok |
| **imdb.com** | B | `CSP` yapılandırması yetersiz |
| **istinye.edu.tr**| C | `HSTS` ve `CSP` tanımlı değil |
| **milliyet.com.tr**| D | Kritik başlıkların çoğu eksik |
| **hurriyet.com.tr**| D | `CSP` ve `HSTS` eksik |
| **n11.com** | C | `X-Frame-Options` hatalı |
| **sahibinden.com**| C | `CSP` başlığı eksik |

## 3. Bulgular ve Teknik Risk Analizi

### 3.1. Content-Security-Policy (CSP)
* **Risk:** CSP bulunmayan siteler, XSS (Cross-Site Scripting) saldırılarına karşı tamamen savunmasızdır. Saldırganlar zararlı scriptleri siteye enjekte edebilir.
* **Doğru Uygulama:** `Content-Security-Policy: default-src 'self';`

### 3.2. HSTS (HTTP Strict Transport Security)
* **Risk:** HSTS eksikliği, sitenin SSL/TLS kullanmasına rağmen saldırganların trafiği HTTP'ye düşürmesine (SSL Stripping) olanak sağlar.
* **Doğru Uygulama:** `Strict-Transport-Security: max-age=63072000; includeSubDomains; preload`

### 3.3. X-Frame-Options (Clickjacking)
* **Risk:** `SAMEORIGIN` başlığının olmaması, sitenin bir iframe içine gizlenerek "Clickjacking" (tıklama hırsızlığı) saldırısına maruz kalmasına neden olur.
* **Doğru Uygulama:** `X-Frame-Options: SAMEORIGIN`

### 3.4. X-Content-Type-Options (MIME Sniffing)
* **Risk:** Bu başlığın eksikliği, tarayıcının yanlış dosya tiplerini yürütmesine ve XSS riskini artırmasına neden olur.
* **Doğru Uygulama:** `X-Content-Type-Options: nosniff`

## 4. Teknik Çözüm: Önerilen Güvenlik Konfigürasyonu
Bir web sunucusu (Nginx/Apache) için en güvenli header seti şudur:

```http
Strict-Transport-Security: max-age=63072000; includeSubDomains; preload;
Content-Security-Policy: default-src 'self'; script-src 'self'; object-src 'none';
X-Frame-Options: DENY;
X-Content-Type-Options: nosniff;
Referrer-Policy: strict-origin-when-cross-origin;
