# # 🛡️ Web Uygulamaları Güvenlik Konfigürasyon Denetimi (Pentest-Audit)

**Hazırlayan:** Fatma Yeliz Apaydın  
**Ders:** BGT208 Güvenli Web Yazılımı Geliştirme

<div align="center">
  <a href="https://istinye.edu.tr">
    <img src="https://istinye.edu.tr/sites/default/files/inline-images/istinye-universitesi-logo.png" alt="Istinye University" width="180"/>
  </a>

  # Web Uygulamaları Güvenlik Konfigürasyon Denetimi (Pentest-Audit)

  ![GitHub](https://img.shields.io/badge/GitHub-Public-green?style=flat-square&logo=github)
  ![Status](https://img.shields.io/badge/Status-Completed-success?style=flat-square)
  ![Course](https://img.shields.io/badge/Course-BGT208-purple?style=flat-square)
</div>

---

## 🎓 Instructor / Danışman
| | |
|---|---|
| **Name** | Keyvan Arasteh |
| **Website** | [qline.tech](https://qline.tech) |

## 👤 Student / Öğrenci
| | |
|---|---|
| **Name** | Fatma Yeliz Apaydın |

## 📚 Course Information / Ders Bilgileri
| | |
|---|---|
| **Course** | Secure Web Development / Güvenli Web Yazılımı Geliştirme |
| **Course Code** | BGT208 |
| **Semester** | 2025-2026 Spring |

---

## 📋 Project Overview / Proje Özeti
Bu proje, 10 farklı popüler web sitesinin **HTTP Güvenlik Başlıkları (Security Headers)** açısından analizini, teknik risk değerlendirmesini ve doğru yapılandırma yöntemlerini içermektedir. Proje, web uygulamalarının siber saldırılara (XSS, MITM, Clickjacking) karşı korunma düzeylerini denetler.



---

## 📊 10 Web Sitesi Analiz Matrisi
Denetim sürecinde uygulanan ölçeklendirme; `SecurityHeaders.com` standartlarına dayanmaktadır.

| Site Adı | Skor | Kritik Başlık Eksiklikleri | Temel Risk |
| :--- | :---: | :--- | :--- |
| **1. google.com** | A+ | Yok | - |
| **2. facebook.com** | A | `Permissions-Policy` | Kısmi API riski |
| **3. github.com** | A | `Permissions-Policy` | Kısmi API riski |
| **4. wikipedia.org** | B | `CSP`, `Permissions-Policy` | XSS & Clickjacking |
| **5. imdb.com** | B | `CSP` yapılandırması | XSS |
| **6. n11.com** | C | `X-Frame-Options` hatalı | Clickjacking |
| **7. sahibinden.com**| C | `CSP` eksik | XSS |
| **8. istinye.edu.tr**| C | `HSTS`, `CSP` eksik | MITM & XSS |
| **9. hurriyet.com.tr**| D | `CSP`, `HSTS` yok | MITM, XSS |
| **10. milliyet.com.tr**| D | `CSP`, `HSTS`, `X-Frame` | Tüm vektörler |

---

## 🛠 Teknik Çözüm ve Hardening (Özet)
Sunucu tarafında uygulanması gereken sıkılaştırılmış konfigürasyon (`src/` altında yer almaktadır):

```nginx
# Örnek Güvenli Nginx Konfigürasyonu
add_header Strict-Transport-Security "max-age=63072000; includeSubDomains; preload" always;
add_header Content-Security-Policy "default-src 'self'; script-src 'self'; object-src 'none';" always;
add_header X-Frame-Options "DENY" always;
add_header X-Content-Type-Options "nosniff" always;
🧪 İspat (PoC) ve Bulgular
Clickjacking: X-Frame-Options barındırmayan siteler iframe içine gömülerek saldırı simüle edilmiştir.

XSS: Content-Security-Policy eksikliği bulunan sitelerde alert() tetiklemesi ile zafiyet ispatlanmıştır.

Detaylar: Tüm ispat çalışmaları ve denetim notları docs/ klasöründe yer almaktadır.

🔗 References / Kaynaklar
SecurityHeaders.com

OWASP Secure Headers Project

Mozilla Web Security Guidelines

Keyvan Arasteh - QLine Tech
